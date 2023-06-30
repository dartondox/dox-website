---
description: >-
  Dox provide several different ways to validate your application's request
  data.
---

# Validation

## Basic Usage

<pre class="language-dart"><code class="lang-dart">import 'package:dox_core/dox_core.dart';

class BlogController {
  create(DoxRequest req) {
<strong>    req.validate({
</strong><strong>      'title': 'required|string|alpha',
</strong><strong>      'body' : 'required|string',
</strong><strong>      'status' : 'required|in:active,draft',
</strong><strong>    });
</strong>
    ....
  }
}
</code></pre>

{% hint style="info" %}
Multiple rules can be separates by vertical bar " | "
{% endhint %}

### Nested Validation

<pre class="language-dart"><code class="lang-dart">import 'package:dox_core/dox_core.dart';

class AddressController {
  create(DoxRequest req) {
    req.validate({
<strong>      'address.city': 'required',
</strong><strong>      'address.post_code': 'required|numeric',
</strong><strong>      'address.street.street_1': 'required',
</strong><strong>      'address.street.street_2': 'required',
</strong>    });

    ....
  }
}
</code></pre>

### Nested with array

<pre class="language-dart"><code class="lang-dart">import 'package:dox_core/dox_core.dart';

class ProductController {
  create(DoxRequest req) {
    req.validate({
<strong>      'product.*.item': 'required',
</strong><strong>      'product.*.price': 'required|double',
</strong><strong>      'product.*.options.*.name': 'required',
</strong><strong>      'product.*.options.*.price': 'required',
</strong>    });

    ....
  }
}
</code></pre>

## Available Rules

<table><thead><tr><th width="255">rule</th><th width="423">example</th></tr></thead><tbody><tr><td><code>required</code></td><td><code>required</code></td></tr><tr><td><code>email</code></td><td><code>email</code></td></tr><tr><td><code>string</code></td><td><code>string</code></td></tr><tr><td><code>numeric</code></td><td><code>numeric</code></td></tr><tr><td><code>boolean</code></td><td><code>boolean</code></td></tr><tr><td><code>integer</code></td><td><code>integer</code></td></tr><tr><td><code>integer</code></td><td><code>integer</code></td></tr><tr><td><code>array</code></td><td><code>array</code></td></tr><tr><td><code>json</code></td><td><code>json</code></td></tr><tr><td><code>ip</code></td><td><code>ip</code></td></tr><tr><td><code>alpha</code></td><td><code>alpha</code></td></tr><tr><td><code>alpha_dash</code></td><td><code>alpha_dash</code></td></tr><tr><td><code>alpha_numeric</code></td><td><code>alpha_numeric</code></td></tr><tr><td><code>date</code></td><td><code>date</code></td></tr><tr><td><code>url</code></td><td><code>url</code></td></tr><tr><td><code>uuid</code></td><td><code>uuid</code></td></tr><tr><td><code>min_length</code></td><td><code>min_length:20</code></td></tr><tr><td><code>max_length</code></td><td><code>max_length:255</code></td></tr><tr><td><code>length_between</code></td><td><code>length_between:100,255</code></td></tr><tr><td><code>between</code></td><td><code>between:18,100</code></td></tr><tr><td><code>min</code></td><td><code>min:18</code></td></tr><tr><td><code>max</code></td><td><code>max:45</code></td></tr><tr><td><code>greater_than</code></td><td><code>greater_than:18</code></td></tr><tr><td><code>less_than</code></td><td><code>less_than:45</code></td></tr><tr><td><code>in</code></td><td><code>in:1,2,3</code></td></tr><tr><td><code>not_in</code></td><td><code>not_in:1,2,3</code></td></tr><tr><td><code>start_with</code></td><td><code>start_wth:dox</code></td></tr><tr><td><code>end_with</code></td><td><code>end_with:framework</code></td></tr><tr><td><code>confirmed</code></td><td><code>confirmed</code></td></tr><tr><td><code>required_if</code></td><td><code>required_if:status,active</code></td></tr><tr><td><code>required_if_not</code></td><td><code>required_if_not:status,active</code></td></tr><tr><td><code>image</code></td><td><code>image:png,jpeg,jpg</code></td></tr><tr><td><code>file</code></td><td><code>file:pdf,jpg,docx</code></td></tr></tbody></table>

### Password Confirmation Validation

<pre class="language-dart"><code class="lang-dart">/// request data
password' => 12345678
password_confirmation' => 12345678

request.validate({
<strong>  'password': 'confirmed'
</strong>});

</code></pre>

As a default it will check with `password_confirmation` field, but you can also use custom name to confirm password.

<pre class="language-dart"><code class="lang-dart">/// request data
password' => 12345678
confirm' => 12345678

request.validate({
<strong>  'password': 'confirmed|confirm'
</strong>});
</code></pre>

### Image Validation

<pre class="language-dart"><code class="lang-dart">/// to allow all images extensions
request.validate({
<strong>  'profile_pic': 'image',
</strong>});

/// to allow only specific image
request.validate({
<strong>  'profile_pic': 'image:png,jpeg,gif,jpg',
</strong>});
</code></pre>

### File Validation

<pre class="language-dart"><code class="lang-dart">/// to allow all file extensions
request.validate({
<strong>  'attachment': 'file',
</strong>});

/// to allow only specific file
request.validate({
<strong>  'attachment': 'file:png,jpeg,pdf,docx',
</strong>});
</code></pre>

### Custom Message

<pre class="language-dart"><code class="lang-dart">request.validate({
    'title': 'required',
    'email': 'required|email',
  }, 
<strong>  messages: {
</strong><strong>    'required' : 'the {attribute} is required',
</strong><strong>    'email' : 'the {value} is not valid email',
</strong><strong>  },
</strong>);
</code></pre>

<table><thead><tr><th width="215">Key</th><th>Description</th></tr></thead><tbody><tr><td><code>{attribute}</code></td><td>This will be replaced with field attribute.</td></tr><tr><td><code>{value}</code></td><td>This will be replace with field value.</td></tr></tbody></table>
