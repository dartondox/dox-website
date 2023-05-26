# ❄ Model

#### Create a new model

<pre><code><strong>$ dox create:model Blog
</strong>$ dart run build_runner build
</code></pre>

#### Create model with migration

<pre><code><strong>$ dox create:model Blog -m
</strong>$ dart run build_runner build
</code></pre>

{% hint style="info" %}
This will create a model inside lib/models folder.&#x20;
{% endhint %}

```dart
import 'package:dox_query_builder/dox_query_builder.dart';
part 'blog.model.g.dart';

@DoxModel()
class Blog extends BlogGenerator {
  @Column()
  String? title;
  
  @Column(name: 'title', beforeSave: makeSlug)
  String? slug;

  @Column()
  String? status;

  @Column(name: 'body')
  String? description;

  @Column(name: 'created_at')
  DateTime? createdAt;

  @Column(name: 'updated_at')
  DateTime? updatedAt;

  static makeSlug(Map<String, dynamic> map) {
    return Slugify().slugify(map['title']);
  }
}
```

{% hint style="info" %}
You can also run build\_runner watch to update changes to generator file.

```bash
$ dart run build_runner watch
```
{% endhint %}

### Table name

```dart
@DoxModel(table: 'blogs')
```

### Primary Key

```dart
@DoxModel(primaryKey: 'uid')
```

### Timestamps column

```dart
@DoxModel(createdAt: 'created_at', updatedAt: 'updated_at')
```

#### Column

```dart
@DoxModel()
class Blog extends BlogGenerator {
  @column()
  String? title

  @column(name: 'user_id')
  String? userId

  @column(beforeSave: getSlugFromTitle)
  String? slug

  @column(name: 'published_at', afterSave: converToHumanReadable)
  DateTime? publishedAt

  static getSlugFromTitle(Map<String, dynamic> map) {
    return slugify(map['title']);
  }

  static converToHumanReadable(Map<String, dynamic> map) {
    var format = DateFormat.yMd('us');
    var dateString = format.format(DateTime.parse(map['published_at']));
  }
}
```



{% hint style="warning" %}
`beforeSave` and `beforeGet` hook must be static function inside\
Model class.
{% endhint %}

#### Soft Deletes

<pre class="language-dart"><code class="lang-dart">@DoxModel()
<strong>class Blog extends BlogGenerator with SoftDeletes {
</strong> // columns here
}
</code></pre>

#### Save

```dart
Actor actor = Actor();
actor.name = 'John Wick';
actor.age = 60;
await actor.save();
```

#### To Map

```dart
Map<String, dynamic> actor = await Actor().find(1).toMap();
```

#### To Json

```dart
String actor = await Actor().find(1).toJson();
```

#### Debug

<pre class="language-dart"><code class="lang-dart">Actor actor = Actor();
actor.name = 'John Wick';
actor.age = 60;
<strong>actor.debug(true);
</strong>await actor.save();
</code></pre>

#### Reset query and create new one

{% hint style="info" %}
If you do not want to create new class and reuse existing class to do new query, use can use `newQuery` attribute.
{% endhint %}

<pre class="language-dart"><code class="lang-dart">Blog blog = Blog();

List&#x3C;Blog> blogs = await blog.where('status', 'active')
    .where('user', 'super_user').get();

// reset existing get query and make new one using `newQuery`
<strong>List&#x3C;Blog> blog = await blog.newQuery
</strong>    .where('status', 'deleted').where('user', 'normal').get();
</code></pre>

#### Hidden columns to response

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class User extends UserGenerator {
  @override
<strong>  List&#x3C;String> get hidden => ['password', 'remember_token'];
</strong>
  ...
}
</code></pre>
