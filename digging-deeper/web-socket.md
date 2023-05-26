# ❄ Web Socket

**Step 1**. Go to `bin/server.dart` and Register websocket in dox

```dart
Dox dox = Dox();

/// Add this Line before initialize
dox.websocket(websocket: DoxWebsocket());

dox.initialize(Config());
```

**Step 2.** Create a controller for web socket as below

```dart
import 'package:dox_core/dox_core.dart';

class SocketController {
  intro(SocketEmitter emitter, message) {
    emitter.room('ABCD').emitExceptSender('intro', message);
  }

  noti(SocketEmitter emitter, message) {
    emitter.room('ABCD').emit('noti', message);
  }
}
```

_Or create using dox-cli_

```bash
$ dox create:controller SocketController -ws
```

**Step 3.** Create a websocket router `websocket.dart` in `lib/routes` folder and add below codes

```dart
import 'package:dox_core/dox_core.dart';
import 'package:dox_sample/http/controllers/socket.controller.dart';

class WebsocketRouter extends Router {
  @override
  register() {
    var controller = SocketController();

    DoxWebsocket.on('intro', controller.intro);
    DoxWebsocket.on('noti', controller.noti);
  }
}
```

**Step 4**. Register `WebsocketRouter` into routers list in `config/app.dart`

```dart
List<Router> get routers => [
    WebsocketRouter()
    WebRouter(), 
    ApiRouter(), 
];
```

{% hint style="info" %}
Websocket url will be on `ws://127.0.0.1:{port}/ws`
{% endhint %}

{% hint style="info" %}
For Handling in client browser, we suggest you to use this library.\
[https://github.com/necessarylion/dox-web-socket-client](https://github.com/necessarylion/dox-web-socket-client)
{% endhint %}

{% hint style="warning" %}
Note: You can also use built in browser `WebSocket` or any client WebSocket library. All you need to follow is when you send data, it must be a json string with `event`, and `message` attribute. See example below.
{% endhint %}

#### Example using `dart:io WebSocket`

<pre class="language-dart"><code class="lang-dart">import 'dart:io';

/// event listening in your routes
/// Eg. DoxWebsocket.on('intro', controller.intro);
String event = 'intro';

// message can be any type such as int, float, json, string etc..
String message = "Hola!"; 

var data = jsonEncode({
<strong>  "event": event,
</strong><strong>  "message": message,
</strong>});

String url = 'ws://localhost:3000/ws';
WebSocket socket = await WebSocket.connect(url);
socket.add(jsonData);
</code></pre>

