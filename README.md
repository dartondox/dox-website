---
description: >-
  A perfect solution for your web backend development with dart, a comprehensive
  and versatile framework that offers a wide range of features to help you build
  powerful and scalable web applications.
---

# Getting Started

## Introduction

Our framework comes equipped with a robust query builder that allows you to easily interact with your database, as well as a model system that simplifies the process of managing your application data. With support for both WebSocket and REST API protocols, you can build real-time applications that are optimized for performance and efficiency. In addition, our database migration system makes it easy to keep your application up-to-date and running smoothly.

We understand the importance of security in web applications, which is why our framework offers built-in support for CORS (Cross-Origin Resource Sharing) to help protect against malicious attacks.&#x20;

But that's not all - our framework also includes a powerful CLI (Command-Line Interface) that enables you to quickly create new projects, models, controllers, and middleware with just a few simple commands. This makes it easy to get started with your web development projects and streamline your workflow.

Overall, our **Dox** - dart web framework is the ultimate solution for developers looking to build high-quality web applications with ease. So why wait? Try it out now and experience the power and flexibility of our framework for yourself!

#### Install Dox CLI

```
$ dart pub global activate dox
```

#### Create new project using dox-cli

```
$ dox create new_blog
$ cd new_blog
$ dart pub get
$ cp .env.example .env (and modify .env variables)
$ dox serve or dox s to start http server
```

{% hint style="warning" %}
Dox framework is currently in alpha state. We will announce fix date for stable release soon. Please join [our discord server](https://discord.gg/tfN9Zs9cxu) for more information.
{% endhint %}

{% hint style="info" %}
If you found any issues or have any suggestion, feel free to create an issue [here](https://github.com/necessarylion/dox-core/issues/new).&#x20;
{% endhint %}

{% hint style="success" %}
Or want to contribute. Fork the repo and create PR to us.
{% endhint %}
