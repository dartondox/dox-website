# Middleware

### Create Middleware

```dart
$ dox create:middlewaer Logger
```

### Class based middleware

```dart
class LoggerMiddleware extends DoxMiddleware {
  @override
  handle(DoxRequest req) {
    print('custom middleware get called');
    return req;
  }
}

var loggerMiddleware = LoggerMiddleware();
Route.get('ping', [loggerMiddleware, webcontroller.pong]);
```

### Function middleware

```dart
authMiddleware(DoxRequest req) {
  return UnAuthorizedException(message: 'Invalid token!');
}

Route.get('ping', [authMiddleware, webcontroller.pong]);art
```

### Multiple middleware

```dart
Route.get('ping', [
    loggerMiddleware,
    authMiddleware,
    webcontroller.pong
]);
```

### Global Middleware

<pre class="language-dart"><code class="lang-dart">class ApiRouter extends Router {
  @override
  String get prefix => 'api';

  @override
<strong>  List get middleware => [LogMiddleware()];
</strong>
  @override
  register() {
    var api = ApiController();

    Route.get('/ping', [api.pong]);

    Route.resource('admins', AdminController());
  }
}
</code></pre>
