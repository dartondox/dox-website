---
description: >-
  Serializer will help you to convert the Model response from controller to your
  custom response and then passed to HttpResponse.
---

# ❄ Serializer

#### Create a serializer

```bash
$ dox create:request Blog
```

#### Usage

Let say we have a blog controller with `getAllBlogs` which return list of blogs and `findBlog` which return singular blog.

<pre class="language-dart"><code class="lang-dart">import 'package:dox_core/dox_core.dart';

class BlogController {
  getAllBlogs(DoxRequest req) async {
     List&#x3C;Blog> blogs = await Blog().all();
<strong>     return BlogSerializer(blogs);
</strong>  }
  
  findBlog(DoxRequest req, id) async {
     Blog blog = await Blog().find(id);
<strong>     return BlogSerializer(blog);
</strong>  }
}
</code></pre>

Dox will convert automatically with the data that you convert in your `BlogSerializer`.

<pre class="language-dart"><code class="lang-dart">import 'package:dox_core/dox_core.dart';

<strong>class BlogSerializer extends Serializer&#x3C;Blog> {
</strong>  BlogSerializer(super.data);

  @override
<strong>  Map&#x3C;String, dynamic> convert(Blog m) {
</strong>    return {
      'id': m.id,
      'title' : m.title,
    };
  }
}
</code></pre>

{% hint style="warning" %}
Please make sure that you have assign your model type in serializer.

extends `Serializer<Blog>`&#x20;
{% endhint %}
