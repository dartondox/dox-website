# Encryption

#### Encode a message

```dart
String encodedMessage = AESEncryptor.encode('Hello world', 'secret');
print(encodedMessage);
```

#### Decode a message

```dart
String decodedMessage = AESEncryptor.decode(encodedMessage, 'secret');
print(decodedMessage);
```
