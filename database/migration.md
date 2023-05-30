# ‣ Migration

#### Create a migration

```bash
$ dox create:migration create_blog_table
```

{% hint style="info" %}
This will generate a migration file inside db/migration folder, where you can update your schema to create, update and drop table.
{% endhint %}

**To create new table**

{% hint style="warning" %}
Dox follow **singular** table name. You can still use custom table name in your model. For more information [check here](model/#table-name).
{% endhint %}

```dart
Schema.create('blog', (Table table) {
  table.id();
  table.string('slug').unique();
  table.string('title').nullable();
  table.string('body').nullable();
  table.timestamps();
});
```

#### To update database table

```dart
await Schema.table('blog', (Table table) {
  // drop/delete amount column
  table.dropColumn('amount');
  
  // rename title to blog_title
  table.renameColumn('title', 'blog_title');
  
  // newly rename blog_title to nullable
  table.string('blog_title').nullable(); 
  
  // change slug to nullable
  table.string('slug').unique().nullable(); 
  
  // add new colum column1
  table.string('column1').nullable(); 
  
  // add new colum column2
  table.string('column2').nullable(); 
});
```

#### To drop or delete table

```dart
Schema.drop('blog');
```

#### Available data types

| Command                           | Description                                          |
| --------------------------------- | ---------------------------------------------------- |
| `table.id()`                      | Incrementing ID                                      |
| `table.string('title')`           | VARCHAR equivalent column                            |
| `table.text('description')`       | TEXT equivalent column                               |
| `table.uuid('uuid')`              | UUID equivalent column                               |
| `table.integer('amount')`         | Integer equivalent column                            |
| `table.bigInteger('amount')`      | BIGINT equivalent column                             |
| `table.char('status')`            | CHAR equivalent column                               |
| `table.money('price')`            | MONEY equivalent column                              |
| `table.json('price')`             | JSON equivalent column                               |
| `table.jsonb('price')`            | JSONB equivalent column                              |
| `table.decimal('price', 11, 2)`   | DECIMAL equivalent column with a precision and scale |
| `table.float4('price')`           | FLOAT4 equivalent column                             |
| `table.float8('price')`           | FLOAT8 equivalent column                             |
| `table.timestamp('approved_at')`  | TIMESTAMP equivalent column                          |
| `table.date('dob')`               | DATE equivalent column                               |
| `table.time('active_time')`       | TIME equivalent column                               |
| `table.timestampTz('created_at')` | TIMESTAMPTZ equivalent column                        |
| `table.softDeletes()`             | Adds **deleted\_at** column                          |
| `table.timestamps()`              | Adds **created\_at** and **updated\_at** columns     |

#### Drop column

```dart
await Schema.table('blog', (Table table) {
  table.dropColumn('amount');
});
```

#### Rename column

```dart
await Schema.table('blog', (Table table) {
  table.renameColumn('old_name', 'new_name');
});
```

**Run migration**

```
$ dox migrate
```

{% hint style="info" %}
Please make sure that you have create `.env` file with with below variable names to run migration.
{% endhint %}

```bash
DB_HOST=localhost
DB_PORT=5432
DB_NAME=postgres
DB_USERNAME=admin
DB_PASSWORD=password
```

**Rollback migration**

```
$ dox migrate:rollback
```
