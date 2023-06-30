# Authentication

### Installation

<pre class="language-yaml"><code class="lang-yaml">dependencies:
  ...
<strong>  dox_auth: &#x3C;latest>
</strong></code></pre>

or

```shell
dart pub add dox_auth
```

### Usage

1. Create auth config `lib/config/auth.dart`

```dart
import 'package:dox_auth/dox_auth.dart';
import 'package:dox_core/dox_core.dart';
import 'package:poc_app/models/user/user.model.dart';

class AuthConfig extends AuthConfigInterface {
  @override
  String get defaultGuard => 'web';

  @override
  Map<String, Guard> get guards => <String, Guard>{
        'web': Guard(
          driver: JwtDriver(
            secret: SecretKey(Env.get('APP_KEY')),
          ),
          provider: Provider(
            model: () => User(),
          ),
        ),
      };
}
```

2. Modify `bin/server.dart` to add auth config

<pre class="language-dart"><code class="lang-dart">Dox dox = Dox();
await dox.initialize(config);
<strong>dox.setAuthConfig(AuthConfig());
</strong></code></pre>

3. Attempt Login

<pre class="language-dart"><code class="lang-dart">Map&#x3C;String, dynamic> credentials = req.only(&#x3C;String>['email', 'password']);

<strong>Auth auth = Auth();
</strong><strong>String? token = await auth.attempt(credentials);
</strong>User? user = auth.user&#x3C;User>();
</code></pre>

4. Register `doxAuthMiddleware` in route

<pre class="language-dart"><code class="lang-dart"> Route.get('/auth/user', &#x3C;dynamic>[
<strong>  doxAuthMiddleware, 
</strong>  authController.user
 ]);
</code></pre>

{% hint style="info" %}
You can also register in global middleware.

```dart
@override
List<dynamic> get middleware => <dynamic>[doxAuthMiddleware];
```
{% endhint %}

5. Verify Logged In or Fetch User information

<pre class="language-dart"><code class="lang-dart">Future&#x3C;dynamic> fetchUser(DoxRequest req) async {
<strong>  Auth? auth = req.auth&#x3C;Auth>();
</strong><strong>  if (auth?.isLoggedIn() == true) {
</strong><strong>    return auth?.user();
</strong>  }
  throw UnAuthorizedException();
}
</code></pre>

#### Expired In&#x20;

```dart
JwtDriver(
  secret: SecretKey(Env.get('APP_KEY')),
  expiresIn: Duration(hours: 5),
),
```

#### Issuer&#x20;

```dart
JwtDriver(
  secret: SecretKey(Env.get('APP_KEY')),
  issuer: 'https://dartondox.dev',
),
```

#### Algorithm&#x20;

```dart
JwtDriver(
  secret: SecretKey(Env.get('APP_KEY')),
  algorithm: JWTAlgorithm.HS256,
),
```

_for more information about algorithm please visit_ [_dart jsonwebstoken_](https://pub.dev/packages/dart\_jsonwebtoken)
