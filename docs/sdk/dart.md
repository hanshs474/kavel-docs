# Dart and Flutter

```bash
dart pub add kavel     # or: flutter pub add kavel
```

```dart
final kavel = Kavel();
final img = await kavel.generate('a glass teapot with blooming flower tea, soft backlight', aspectRatio: '4:5');
print(img.url);
```

Without a key there is no secret to ship inside an app. With `apiKey:` calls run on your account — keep
that path on your server. See [Using an API key](../api-key.md).

Source: [github.com/hanshs474/kavel-dart](https://github.com/hanshs474/kavel-dart) · [pub.dev/packages/kavel](https://pub.dev/packages/kavel)
