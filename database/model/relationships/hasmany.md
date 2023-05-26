# ❄ HasMany

```dart
@DoxModel()
class Comment extends CommentGenerator {
  @Column()
  String? message
}


@DoxModel()
class Blog extends BlogGenerator {
  ... 

  @HasMany(Comment)
  Comment? comments;

  @HasMany(Comment, onQuery: filterApprovedComment)
  Comment? approvedComments;

  static filterApprovedComment(Comment cmt) {
    return cmt.where('status', 'approved');
  }
}
```

```dart
class HasMany {
  final Type model;
  final String? foreignKey;
  final String? localKey;
  final Function? onQuery;
  final bool? eager;

  const HasMany(this.model,
      {this.foreignKey, this.localKey, this.onQuery, this.eager});
}
```



<table><thead><tr><th width="189">column</th><th></th></tr></thead><tbody><tr><td>model</td><td>Related model </td></tr><tr><td>foreignKey</td><td><code>blog_id</code> in our case</td></tr><tr><td>localKey</td><td><code>id</code> in our case</td></tr><tr><td>onQuery</td><td>Add custom query to related model</td></tr><tr><td>eager</td><td>Load relation automatically on getting record.</td></tr></tbody></table>
