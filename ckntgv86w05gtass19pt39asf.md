## Local Push Notification in Flutter

Hello everyone, Today I'll show you how we can implement local push notification in a flutter app.

## Implementation

We will use a package called  [flutter_local_notifications](https://pub.dev/packages/flutter_local_notifications) .

Add the following to your ` pubspec.yaml ` file:

```yaml
dependencies:
  ....
  flutter_local_notifications: ^5.0.0+1
``` 


> Check for the latest version in the package link.

Add the following to your ` AndroidManifest.xml ` file:

```xml
<uses-permission 
  android:name="android.permission.VIBRATE" />
<uses-permission 
  android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
``` 
> Taking permission to schedule notification and for vibration.

### Local Notification Helper
Create a file named as ` LocalNotificationHelper.dart `.

> You can give any name to the file. I prefer the filenames to be specific with their functionality.

Will do everything inside a class named ` LocalNotificationHelper ` and don't forget to import our ` flutter_local_notifications ` plugin.


```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class LocalNotificationHelper {
  final FlutterLocalNotificationsPlugin _flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();
  static LocalNotificationHelper _localNotification;

  LocalNotification._createInstance();
  factory LocalNotificationHelper() {
    if (_localNotification == null) {
      _localNotification = LocalNotificationHelper._createInstance();
      _localNotification._initialize();
    }
    return _localNotification;
  }
}
``` 

> First we are creating the instance of ` FlutterLocalNotificationsPlugin `.
> Then creating the instance of our class ` LocalNotificationHelper ` with a  [singleton pattern](https://blog.bibekkakati.me/implementing-singleton-pattern-in-dart-flutter) .

Now we will implement ` onSelectNotification` and ` onDidReceiveLocalNotification ` method that will get invoked on pressing the notification on ` Android ` and ` iOS ` respectively.

```dart
....
class LocalNotificationHelper {
  ....
  Future _onSelectNotification(String payload) async {
    // Implement your own logic
  }

  Future _onDidReceiveLocalNotification(
      int id, String title, String body, String payload) async {
    // Implement your own logic
  }
}
``` 

Sometimes we want to decouple these helper files from our UI and functionality, in that case, you can set these ` onSelectNotification` and ` onDidReceiveLocalNotification ` methods from outside by passing them as an argument to another method of this helper class like this:

```dart
....
class LocalNotificationHelper {
  ....
  var _onSelectNotification, _onDidReceiveLocalNotification;
  void init(onSelectNotification, onDidReceiveLocalNotification) {
    if (this._onSelectNotification == null) {
      this._onSelectNotification = onSelectNotification;
    }
    if (this._onDidReceiveLocalNotification == null) {
      this._onDidReceiveLocalNotification= onDidReceiveLocalNotification;
    }
  }
}
``` 

> Now we can call this ` init ` method from our ` main.dart ` or ` Homepage `. Don't forget to pass the methods.

We will now initialize our notification settings.
Let's create a ` _initialize ` method inside our class.

```dart
....
class LocalNotificationHelper {
  ....
  Future<void> _initialize() async {
    AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('@drawable/ic_notification');

    IOSInitializationSettings initializationSettingsIOS =
        IOSInitializationSettings(
            onDidReceiveLocalNotification: _onDidReceiveLocalNotification);

    InitializationSettings initializationSettings = InitializationSettings(
        android: initializationSettingsAndroid, iOS: initializationSettingsIOS);

    await _flutterLocalNotificationsPlugin.initialize(initializationSettings,
        onSelectNotification: _onSelectNotification);
  }
}
``` 

` AndroidInitializationSettings ` and ` IOSInitializationSettings ` are initializing the settings for ` Android ` and ` iOS ` platform respectively.

We can also pass the path of the default notification icon in ` AndroidInitializationSettings `.

### Showing Notification

Let's create a ` showNotification ` method, which will pop a notification.  You can call this method from anywhere to create a push notification.

```dart
....
class LocalNotificationHelper {
  ....
  Future<void> showNotification() async {
    const AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'channel id',
      'channel name',
      'channel description',
      importance: Importance.max,
      priority: Priority.high,
      icon: '@drawable/ic_notification',
    );
    const IOSNotificationDetails iOSPlatformChannelSpecifics =
        IOSNotificationDetails();
    const NotificationDetails platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);
    await _flutterLocalNotificationsPlugin.show(
        0, 'Notification Title', 'Notification Body', platformChannelSpecifics,
        payload: 'Notification Payload');
  }
}
``` 
` AndroidNotificationDetails ` is responsible for configuring the notification for a specific channel in android devices. If you go to the notification section inside the app info of your app, you will see this ` channel name ` there. Also, we can set priority, vibration, importance etc.
` show ` method is responsible for creating the push notification. It expects some arguments like ` id, title, body, payload `.

> `title` and `body` will be visible in the actual notification popup and `payload` will be available on `onSelectNotification` method.

### Schedule Notification

Let's create a ` scheduleNotification ` method, which will schedule the notification to pop at a specific time.  You can call this method from anywhere to schedule a push notification.

```dart
....
class LocalNotificationHelper {
  ....
  Future<void> scheduleNotification() async {
    const AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'channelId',
      'channelName',
      'channelDescription',
      importance: Importance.max,
      priority: Priority.high,
      icon: '@drawable/ic_notification',
    );
    const IOSNotificationDetails iOSPlatformChannelSpecifics =
        IOSNotificationDetails();
    const NotificationDetails platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);
    await _flutterLocalNotificationsPlugin.schedule(
        0, 'Notification Title', 'Notification Body', DateTime.now(), platformChannelSpecifics,
        payload: 'Notification Payload');
  }
}
``` 

> ` schedule ` method is similar to the ` show ` method with just one additional positional argument that is the time at which you want to push that notification to the user.

### Cancel Notification

Let's create a ` cancelNotification ` method, which will cancel the scheduled notification. 

```dart
....
class LocalNotificationHelper {
  ....
  Future<void> cancelNotification() async {
    await _flutterLocalNotificationsPlugin.cancel(0);
  }
}
``` 
> ` cancel` method expects the ` id ` of the notification as an argument.

### Cancel All Notification

Let's create a ` cancelAllNotification ` method, which will cancel all the scheduled notifications. 

```dart
....
class LocalNotificationHelper {
  ....
  Future<void> cancelAllNotification() async {
    await _flutterLocalNotificationsPlugin.cancelAll();
  }
}
``` 


### Repetitive Notification

Let's create a ` repeatNotification ` method, which will push the notification at an interval of time. 

```dart
....
class LocalNotificationHelper {
  ....
  Future<void> repeatNotification() async {
    const AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'channelId',
      'channelName',
      'channelDescription',
      importance: Importance.max,
      priority: Priority.high,
      icon: '@drawable/ic_notification',
    );
    const IOSNotificationDetails iOSPlatformChannelSpecifics =
        IOSNotificationDetails();
    const NotificationDetails platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);
    await _flutterLocalNotificationsPlugin.periodicallyShow(
        0, 'Notification Title', 'Notification Body', RepeatInterval.daily, platformChannelSpecifics,
        payload: 'Notification Payload');
  }
}
``` 
> ` periodicallyShow ` method is similar to the ` schedule` method but it takes a  [RepeatInterval](https://pub.dev/documentation/flutter_local_notifications_extended/latest/flutter_local_notifications_extended/RepeatInterval-class.html)  type of argument.

### Pending Notifications

Let's create a ` getPendingNotifications ` method, which will retrieve all the pending notifications. 

```dart
....
class LocalNotificationHelper {
  ....
  Future<List<PendingNotificationRequest>> getPendingNotifications () async {
    return await _flutterLocalNotificationsPlugin.pendingNotificationRequests();
  }
}
``` 

We can do a lot more with the properties of notification like showing media, pictures etc.

I have personally used this local push notification in some of my apps and I must say it works perfectly well. Scheduled Notification is fast and reliable but there are some caveats, you can read it  [here](https://pub.dev/packages/flutter_local_notifications#-caveats-and-limitations).

> Haven't tested with iOS device.

---


Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)
