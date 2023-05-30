---
description: Cross-Origin Resource Sharing
---

# ‣ CORS

CORS configuration can be found in `lib/config/app.dart`

```dart
class Config implements AppConfig {
   ...

   @override
   CORSConfig get cors => CORSConfig(
      allowOrigin: '*',
      allowMethods : ['GET', 'POST'],
      allowHeaders : '*'
      exposeHeaders : 'Authorization',
      allowCredentials: true,
      maxAge : Duration(hours: 1).inSeconds
   );

   ...
}
```

| Option             | Type                     |
| ------------------ | ------------------------ |
| `allowOrigin`      | `List<String> or String` |
| `allowMethods`     | `List<String> or String` |
| `allowHeaders`     | `List<String> or String` |
| `exposeHeaders`    | `List<String> or String` |
| `allowCredentials` | `bool`                   |
| `maxAge`           | `int`                    |

