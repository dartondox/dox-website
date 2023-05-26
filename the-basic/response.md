# ❄ Response

```dart
import 'package:dox_core/dox_core.dart';

// string
class BlogController {
  index(DoxRequest req) {
    return 'pong';
  }
}

// exception
class BlogController {
  index(DoxRequest req) {
    return InternalErrorException();
  }
}

// map
class BlogController {
  index(DoxRequest req) {
    return {"message" : "hellow world"};
  }
}

// Model
class BlogController {
  index(DoxRequest req) {
    Admin admin = await Admin().find(1)
    return admin;
  }
}

// List<Model>
class BlogController {
  index(DoxRequest req) {
    List admins = await Admin().all()
    return admins;
  }
}
```

### Response with headers

```dart
return response()
  .header('Authorization', 'Bearer xxxxxx')
  .header('ContentType', 'application/json');
      
/// or

return response().withHeaders({
    'Authorization' : 'Bearer xxxxxx',
    'ContentType', 'application/json'
});
```

### Status Code

```dart
return response().statusCode(401);
```

### Content Type

```dart
return response().contentType(ContentType.json);
```

### Cookie

#### Set cookie

```dart
var cookie = DoxCookie('key', 'value');
return response().cookie(cookie);
```

{% hint style="info" %}
As a default cookie value will be encrypted with `APP_KEY` \
you can disable by setting `encrypt: false`&#x20;
{% endhint %}

#### get cookie

```dart
controllerFunction(DoxRequest req) {
    cookie = req.cookie(key)
}
```

{% hint style="info" %}
As a default cookie value will be get back by decrypted with `APP_KEY` \
you can disable by setting `decode: false`&#x20;
{% endhint %}
