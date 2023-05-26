---
description: >-
  Let say we have blog and comment table where each blog can have multiple
  comments. So each comment is belongs to specific blog.
---

# ❄ BelongsTo

```dart
@DoxModel()
class Blog extends BlogGenerator {
  @Column()
  String? title
}


@DoxModel()
class Comment extends CommentGenerator {
  ... 

  @BelongsTo(Blog, eager: true)
  Blog? blog;
}
```

```dart
class BelongsTo {
  final Type model;
  final String? foreignKey;
  final String? localKey;
  final Function? onQuery;
  final bool? eager;

  const BelongsTo(this.model,
      {this.foreignKey, this.localKey, this.onQuery, this.eager});
}
```



<table><thead><tr><th width="189">column</th><th></th></tr></thead><tbody><tr><td>model</td><td>Related model </td></tr><tr><td>foreignKey</td><td><code>blog_id</code> in our case</td></tr><tr><td>localKey</td><td><code>id</code> in our case</td></tr><tr><td>onQuery</td><td>Add custom query to related model</td></tr><tr><td>eager</td><td>Load relation automatically on getting record.</td></tr></tbody></table>
