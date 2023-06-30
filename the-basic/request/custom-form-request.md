# Custom Form Request

### Create a request

```bash
$ dox create:request Blog
```

### Usage

```dart
import 'package:dox_core/dox_core.dart';

class BlogRequest extends FormRequest {
  String? title;
  String? description;

  @override
  void setUp() {
    title = input('title');
    description = input('desc');
  }

  @override
  Map<String, String> rules() {
    return {
      'title': 'required',
    };
  }

  @override
  Map<String, String> messages() {
    return {};
  }
}
```

Register `BlogRequest` in `lib/config/app.dart`&#x20;

{% hint style="info" %}
Since there is no way to create a class from string in dart unless we use `dart:mirrors`, we need to register your request class in `app.dart` . And dox will automatically pass this request  to controller.
{% endhint %}

<pre class="language-dart"><code class="lang-dart">@override
  Map&#x3C;Type, Function()> get formRequests => {
<strong>    BlogRequest:() => BlogRequest(),
</strong>  };

</code></pre>

Finally use from controller

<pre class="language-dart"><code class="lang-dart">class BlogController {
    store(BlogRequest req) async {
        Blog blog = Blog();
        
<strong>        blog.title = req.title;
</strong><strong>        blog.description = req.description;
</strong>        
        await blog.save();
        return blog;
    }
}
</code></pre>

You can now access title and description from controller with auto suggestion. \
And validation rules that you assign in BlogRequest will be apply automatically.\


