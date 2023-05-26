---
description: >-
  dox is a cli tool to generate migration, model and to handle database
  migration. It support up and down methods to control migration version.
---

# ❄ Dox CLI

### Activate

```bash
$ dart pub global activate dox
```

{% hint style="info" %}
Please make sure you have included bin path to your profile. If you did not added path to your profile yet, open `~/.bashrc` or `~/.zshrc` and paste below line.
{% endhint %}

```dart
export PATH="$PATH":"~/.pub-cache/bin"
```

### Update dox

```
$ dox update
```

### **Commands**

#### Create Project

```
$ dox create new_blog
```

**Serve Project**

```
$ dox serve 
or 
$ dox s

$ dox s --ignore-build-runner // ignore build runner watch
```

**Run build runner**

```
$ dox build_runner:watch
$ dox build_runner:build
```

**Build project for production**

```
$ dox build (compile into machine code)
$ bin/dox (run exec file to serve http server)
```

#### Generate app key

```
$ dox key:generate
```

#### Create controller

```
$ dox create:controller admin_controller
```

> to create resource controller

```
$ dox create:controller admin_controller -r
```

> to creater websocket controller

```
$ dox create:controller socket_controller -ws
```

#### Create Middleware

```
$ dox create:middleware auth_middleware
```

**Create migration**

```
$ dox create:migration create_foo_table
```

**Create model**

```
$ dox create:model ModelName
```

**Create model with migration**

```
$ dox create:model User -m
```

**Run migration**

```
$ dox migrate
```

{% hint style="info" %}
Please make sure that you have create `.env` file with with below variable names to run migration.
{% endhint %}

```bash
DB_HOST=localhost
DB_PORT=5432
DB_NAME=postgres
DB_USERNAME=admin
DB_PASSWORD=password
```

**Rollback migration**

```
$ dox migrate:rollback
```

### Deactivate CLI

```
$ dart pub global deactivate dox
```
