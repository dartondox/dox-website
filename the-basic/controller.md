# Controller

### Create a controller

```dart
$ dox create:controller Blog
```

```dart
import 'package:dox_core/dox_core.dart';

class BlogController {
  index(DoxRequest req) {
    return 'pong';
  }
}
```

### Create a resource controller

```dart
$ dox create:controller Blog -r
```

```dart
import 'package:dox_core/dox_core.dart';

class BlogController {
  /// GET /resource
  index(DoxRequest req) async {}

  /// GET /resource/create
  create(DoxRequest req) async {}

  /// POST /resource
  store(DoxRequest req) async {}

  /// GET /resource/{id}
  show(DoxRequest req, String id) async {}

  /// GET /resource/{id}/edit
  edit(DoxRequest req, String id) async {}

  /// PUT|PATCH /resource/{id}
  update(DoxRequest req, String id) async {}

  /// DELETE /resource/{id}
  destroy(DoxRequest req, String id) async {}
}
```

