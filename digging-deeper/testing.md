# Testing

<pre class="language-dart"><code class="lang-dart">import 'package:http/http.dart' as http;

Config config = Config();
String baseUrl = 'http://localhost:${config.serverPort}';

void main() {
    setUpAll(() async {
<strong>      Dox().initialize(config);
</strong><strong>      Database().setup(config);
</strong><strong>      await Future.delayed(Duration(milliseconds: 500));
</strong>    });

    tearDownAll(() {
<strong>      Dox().server.close();
</strong>    });

    test('ping route', () async {
<strong>      var url = Uri.parse('$baseUrl/ping');
</strong>      var response = await http.get(url);
      expect(response.statusCode, 200);
      expect(response.body, 'pong');
    });
}
</code></pre>
