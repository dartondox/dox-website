---
description: Dox Hash class allow you to hash the value using bcrypt.
---

# Hashing

#### Hash a password&#x20;

```dart
 String secret = 'password';
 String hashedPassword = Hash.make(secret);
```

#### Verify hashed password

```dart
String secret = 'password';
bool verified = Hash.verify(secret, hashedPassword);
```
