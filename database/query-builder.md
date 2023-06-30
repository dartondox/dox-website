# Query Builder

{% hint style="info" %}
Easy query builder to do CRUD operations.
{% endhint %}

### Insert or create

```dart
// single entry
await Actor().create(
  {'name': 'John Wick', 'age': 60}
);

await Actor().insert(
  {'name': 'John Wick', 'age': 60}
);

// multiple
await Actor().insertMultiple([
  {'name': 'John Wick', 'age': 60},
  {'name': 'John Doe', 'age': 25},
]);
```

### Update

```dart
await Actor()
  .where('id', 3)
  .where('status', 'active')
  .update({
    "name": "Updated AJ",
    "age": 120,
  });
```

### Count

```dart
await Actor().count();

await Actor().where('age', '>=' , 23).count();
```

### Find

```dart
await Actor().find(id); // find by id

await Actor().find('name', 'John Wick');
```

### Get First

```dart
Actor actor = await Actor().getFirst(); // limit 1
```

### All

```dart
List<Actor> actors = await Actor().all();
for(Actor actor in actors) {
  print(actor.id)
}
```

### Get

```dart
List<Actor> actors = await Actor().where('name', 'John Wick').get();
for(Actor actor in actors) {
  print(actor.id)
}
```

### To SQL

```dart
String query = Actor().where('name', 'John Wick').toSql();
print(query)
```

### Delete

```dart
await Actor().where('name', 'John Wick').delete();
```

### Force delete (only with SoftDeletes)

```dart
await Actor().where('name', 'John Wick').forceDelete();
```

### With Trash (only with SoftDeletes)

```dart
List actors = await Actor().where('name', 'John Wick').withTrash().get();
for(Actor actor in actors) {
  print(actor.id)
}
```

### Select

```dart
await Actor()
  .select('id')
  .select('name')
  .where('name', 'John Wick').get();

await Actor()
  .select(['id', 'name', 'age']).where('name', 'John Wick').get();

await Actor()
  .select('id, name, age').where('name', 'John Wick').get();
```

### Where In

```dart
await Actor().whereIn('id', ['1', '2']).get();
```

### Where

```dart
// equal condition between column and value
await Actor().where('name', 'John Wick').get();

// custom condition between column and value
await Actor().where('name', '=', 'John Wick').get();
await Actor().where('age', '>=', 23).get();
```

### Or where

```dart
// equal condition between column and value
await Actor().orWhere('name', 'John Wick').get();

// custom condition between column and value
await Actor().orWhere('name', '=', 'John Wick').get();
await Actor().orWhere('age', '>=', 23).get();
```

### Where raw

```dart
await Actor().whereRaw('name = @name', {'name', 'John Wick'}).get();
```

### Or where raw

```dart
await Actor().orWhereRaw('name = @name', {'name', 'John Wick'}).get();
```

### Chain where and or where

```dart
await Actor()
  .where('name', 'John Doe').orWhere('name', 'John Wick').get();
```

### Limit or take

```dart
await Actor().limit(10).get();
// or
await Actor().take(10).get();
```

### Offset

```dart
await Actor().limit(10).offset(10).get();
```

### Group by

```dart
await Actor()
  .select('count(*) as total, name').groupBy('name').get();
```

### Order by

```dart

// default order by with name column
await Actor().orderBy('name').get();

// order by column and type desc
await Actor().orderBy('name', 'desc').get();

// order by column and type asc
await Actor().orderBy('name', 'asc').get();

// multiple order by
await Actor()
  .orderBy('name', 'asc')
  .orderBy('id', 'desc')
  .get();
```

### Join

```dart
await Actor()
    .join('actor_info', 'actor_info.admin_id', 'admin.id')
    .get();
```

### Left join

```dart
await Actor()
    .leftJoin('actor_info', 'actor_info.admin_id', 'admin.id')
    .get();
```

### Right join

```dart
await Actor()
    .rightJoin('actor_info', 'actor_info.admin_id', 'admin.id')
    .get();
```

### Join raw

```dart
await Actor()
    .joinRaw('actor_info on actor_info.admin_id = admin.id')
    .get();
```

### Left join raw

```dart
await Actor()
    .leftJoinRaw('actor_info on actor_info.admin_id = admin.id')
    .get();
```

### Right join raw

```dart
await Actor()
    .rightJoinRaw('actor_info on actor_info.admin_id = admin.id')
    .get();
```

### Debug

```dart
await Actor().debug(true).all();
```
