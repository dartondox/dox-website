# Request

### Request body

<pre class="language-dart"><code class="lang-dart">/// req.body

class ApiController {
  sayHello(DoxRequest req) {
<strong>    String name = req.body['name']
</strong>    return 'Hello $name';
  }
}
</code></pre>

### Param

<pre class="language-dart"><code class="lang-dart">/// req.param

Route.get('/hello/{name}');

class ApiController {
<strong>  sayHello(DoxRequest req, String name) {
</strong>    return 'Hello $name';
  }
}
</code></pre>

### Form Data File

```dart
class ApiController {
  uploadImage(DoxRequest req, String name) {
    req.validate({
      'image': 'required|image:png,jpg',
    });
    
    RequestFile image = req.input('image');
    String uploadedPath = await image.store();
    
    return {"filename" : uploadedPath};
  }
}
```

### Functions

#### `req.query`

```dart
/// if url is https://example.com?name=John
String name = req.query['name']
```

#### `req.input()`

```dart
/// you can get body and query values with input()
String name = req.input('name');
```

#### `req.only()`

```dart
Map<String, dynamic> params = req.only(['email', 'name']);
```

#### `req.ip()`

```dart
// get user IP address
String ip = req.ip(); 
```

#### `req.header()`

```dart
// get header value
String authToken = req.header('Authorization') 
```

#### `req.has()`

```dart
if(req.has('email')) {
 // do something
}
```

#### `req.all()`

```dart
/// req.all() will combine query and body inputs
Map<String, dynamic> inputs = req.all();
```

### Add extra key to request&#x20;

```dart
/// this is useful when you want to add extra param 
/// to request payload in the middleware
req.add('foo', bar);
```

Or you can also merge multiple extra key to request

```dart
req.merge({"foo" : bar, "kit" : kat});
```

### Request Method

<pre class="language-dart"><code class="lang-dart">class ApiController {
  showMethod(DoxRequest req) {
<strong>    return req.method; // GET | POST etc..
</strong>  }
}
</code></pre>

### Get Cookie

```dart
req.cookie('authKey');
```

### Request URI

<pre class="language-dart"><code class="lang-dart">class ApiController {
  showUriPath(DoxRequest req) {
<strong>    Uri uri = req.uri;
</strong>    return uri.path;
  }
}
</code></pre>

#### Get original HttpRequest from dart:io

```dart
HttpRequest ioReq = req.httpRequest;
```

### Others

<table><thead><tr><th width="245">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>req.userAgent()</code></td><td>Get user agent informatin</td></tr><tr><td><code>req.host()</code></td><td>Get host or domain</td></tr><tr><td><code>req.origin()</code></td><td>Get origin of the request</td></tr><tr><td><code>req.referer()</code></td><td>Get referer information from request</td></tr><tr><td><code>req.isFormData()</code></td><td>Check request is form-data</td></tr><tr><td><code>req.isJson()</code></td><td>Check request is json/application</td></tr></tbody></table>
