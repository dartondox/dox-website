# ❄ HasOne

```dart
@DoxModel()
class UserInfo extends UserInfoGenerator {
 @Column()
 String? address;

 @Column(name: 'house_number')
 String? houseNumber;
}


@DoxModel()
class User extends UserGenerator {
  ...

  @HasOne(UserInfo)
  UserInfo? userInfo;
}
```

```dart
class HasOne {
  final Type model;
  final String? foreignKey;
  final String? localKey;
  final Function? onQuery;
  final bool? eager;

  const HasOne(this.model,
      {this.foreignKey, this.localKey, this.onQuery, this.eager});
}
```

<table><thead><tr><th width="189">column</th><th></th></tr></thead><tbody><tr><td>model</td><td>Related model </td></tr><tr><td>foreignKey</td><td><code>user_id</code> in our case</td></tr><tr><td>localKey</td><td><code>id</code> in our case</td></tr><tr><td>onQuery</td><td>Add custom query to related model</td></tr><tr><td>eager</td><td>Load relation automatically on getting record.</td></tr></tbody></table>
