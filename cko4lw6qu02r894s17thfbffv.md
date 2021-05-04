## Secure Local Storage in Flutter

In this article,  you will learn how to implement secure local storage in flutter apps.

If you have experience with front-end web development, you know we use the browser's local storage to store data in key-value pairs. Similarly, we can store data in flutter apps too, but this implementation's under the hood working is a little different as data is getting encrypted.

- Keychain is used for iOS.
- AES encryption is used for Android. AES secret key is encrypted with RSA and RSA key is stored in KeyStore.

> KeyStore was introduced in Android 4.3 (API level 18). The plugin wouldn't work for earlier versions.

## Implementation
We will use a flutter plugin called  [flutter_secure_storage](https://pub.dev/packages/flutter_secure_storage) .

Add the following to your ` pubspec.yaml ` file:

```
dependencies:
  ...
  flutter_secure_storage: ^4.2.0
``` 

> Check for the latest version on the plugin's page.

### Configure Android Version

In `[project]/android/app/build.gradle` set `minSdkVersion` to >= 18.

```
android {
  ...
  defaultConfig {
    ...
    minSdkVersion 18
    ...
  }
}
``` 
### Create Instance

Import `flutter_secure_storage` in your file and create an instance of it.


```
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

FlutterSecureStorage _localStorage = new FlutterSecureStorage();
``` 

### Write Data

To insert a key-value pair in the storage, we will use the `write` method.
We need to pass `key` and `value` to this method.

```
await _localStorage.write(key: key, value: value);
``` 

- `key` and `value` should be a string.
- If the `key` already exists, the `value` will get replaced.
- If we pass a `null` value and the `key` already exists, it will get deleted.
- Its return type is `void`.

### Read Data

To read a `value` for a particular `key`, we will use the `read` method.
We need to pass the `key` to this method.

```
await _localStorage.read(key: key);
``` 

- `key` should be a string.
- If the `key` exists, the `value` will be returned.
- If the `key` doesn't exist the `null` will be returned.
- Its return type is always a string.

### Read All Data

To read all the values, we will use the `readAll` method.

```
await _localStorage.readAll();
``` 

- It will return all the key-value pairs as a `Map`.

### Delete Data

To delete an entry, we will use the `delete` method.
We need to pass the `key` to this method.

```
await _localStorage.delete(key: key);
``` 

- `key` should be a string.
- Its return type is `void`.

### Delete All Data

To delete all entries, we will use the `deleteAll` method.

```
await _localStorage.deleteAll();
``` 

- Its return type is void.

Thank you for reading. Give it a thumbs-up if it is helpful for you.

Feel free to  [connect](https://bibekkakati.me) 👋

<a href="https://www.buymeacoffee.com/bibekkakati" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

