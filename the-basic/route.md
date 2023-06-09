# Route

> Routes can be found in `lib/routes` folder.\
> `api.dart` is with prefix `api`

## Supported Routes

<table><thead><tr><th width="145">Method</th><th>Function</th></tr></thead><tbody><tr><td>GET</td><td><code>Route.get(routeName, controller.method)</code></td></tr><tr><td>POST</td><td><code>Route.post(path, controller.method)</code></td></tr><tr><td>PUT</td><td><code>Route.put(path, controller.method)</code></td></tr><tr><td>PATCH</td><td><code>Route.patch(path, controller.method)</code></td></tr><tr><td>DELETE</td><td><code>Route.delete(path, controller.method)</code></td></tr><tr><td>COPY</td><td><code>Route.copy(path, controller.method)</code></td></tr><tr><td>HEAD</td><td><code>Route.head(path, controller.method)</code></td></tr><tr><td>OPTIONS</td><td><code>Route.options(path, controller.method)</code></td></tr><tr><td>LINK</td><td><code>Route.link(path, controller.method)</code></td></tr><tr><td>UNLINK</td><td><code>Route.unlink(path, controller.method)</code></td></tr><tr><td>PURGE</td><td><code>Route.purge(path, controller.method)</code></td></tr><tr><td>LOCK</td><td><code>Route.lock(path, controller.method)</code></td></tr><tr><td>UNLOCK</td><td><code>Route.unlock(path, controller.method)</code></td></tr><tr><td>VIEW</td><td><code>Route.view(path, controller.method)</code></td></tr></tbody></table>

### Route Param

```dart
Route.get('/blog/{id}', info);
Route.get('/blog/{id}/activate', activate);

info(DoxRequest req, String id) {

}

activate(DoxRequest req, String id) {

}
```

### Group Route

<pre class="language-dart"><code class="lang-dart"><strong>Route.group(prefix, () {
</strong>    Route.get(path, controller);
    Route.post(path, controller);
});
</code></pre>

### Domain Route

<pre class="language-dart"><code class="lang-dart"><strong>Route.domain('dartondox.com', () {
</strong>    Route.get(path, controller);
    Route.post(path, controller);
});
</code></pre>

### Route Middleware

```dart
Route.middleware([CustomMiddleware()], () {
    Route.get(path, controller);
    Route.post(path, controller);
});
```

### WebSocket Route

```dart
Router.websocket('ws', (socket) {
    socket.on('event', controller.intro);
    socket.on('noti', controller.noti);
});
```

### Resource Route

```dart
Route.resource('blogs', BlogController());
```

<table><thead><tr><th width="146.33333333333331">Method</th><th width="238">URI</th><th>Controller Function</th></tr></thead><tbody><tr><td>GET</td><td><code>/blogs</code></td><td>index</td></tr><tr><td>GET</td><td><code>/blogs/create</code></td><td>create</td></tr><tr><td>POST</td><td><code>/blogs</code></td><td>store</td></tr><tr><td>GET</td><td><code>/blogs/{id}</code></td><td>show</td></tr><tr><td>GET</td><td><code>/blogs/{id}/edit</code></td><td>edit</td></tr><tr><td>PUT/PATCH</td><td><code>/blogs/{id}</code></td><td>update</td></tr><tr><td>DELETE</td><td><code>/blogs/{id}</code></td><td>destroy</td></tr></tbody></table>

## Usage

### Callback

```dart
Route.get('/ping', (DoxRequest req) => 'pong');
```

### &#x20;Controller

```dart
class WebController {
 pong(DoxRequest req) async {
   return 'pong';
 }
}

var webController = WebController();
Route.get('ping', webcontroller.pong);
/// or 
Route.get('ping', [webcontroller.pong]);
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

#### <mark style="color:green;">Do (Good practice)</mark>

```dart
var webController = WebController();

Route.get('/ping', webController.ping);
Route.get('/index', webController.index);
Route.get('/create', webController.create);
```

#### <mark style="color:red;">Don't (Bad practice)</mark>

```dart
Route.get('/ping', WebController().ping);
Route.get('/index', WebController().index);
Route.get('/create', WebController().create);
```

{% hint style="danger" %}
Do not create multiple instance of WebController, instead create only one instance and use in other routes.
{% endhint %}
