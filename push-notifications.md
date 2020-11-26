# The stack

* [react-native-navigation](https://github.com/wix/react-native-navigation) by Wix
* [react-native-notifications](https://github.com/wix/react-native-notifications) by Wix
* [@react-native-firebase/messaging](https://rnfirebase.io/messaging/usage) to work with firebase

# Useful articles

You can start from [Best Practices for Push Notifications in React Native](https://www.wix.engineering/post/best-practices-for-push-notifications-in-react-native), and then check [repo](https://github.com/yogevbd/PushNotificationsTutorial) for the whole code from this article.

Also, FireBase has a good article about setting up all iOS required stuff:
[iOS Messaging Setup](https://rnfirebase.io/messaging/usage/ios-setup)

After doing this right, you will have a working Push Notification, and it's enough for you in case if you will not use Firebase Cloud Messaging.

Honestly, it will work with Firebase too, but you will not receive notifications in the Foreground app state (at least for the moment, when I'm writing this). To get this to work, you can use this little hack:


``` js
import { Notifications } from 'react-native-notifications';
import messaging from '@react-native-firebase/messaging';

const sendLocalNotification = (notification) => {
  const id = parseInt(notification.messageId);

  Notifications.postLocalNotification(
    {
      body: notification.notification.body,
      title: notification.notification.title,
      userName: notification.data.userName,
      userId: notification.data.userId,
    },
    id,
  );
};

useEffect(() => {

  Notifications.events().registerNotificationReceivedForeground((notification, completion) => {
    console.log(`Notification received in foreground:${JSON.stringify(notification)}`);
    completion({ alert: true, sound: true, badge: true });
  });

  messaging()
    .getToken()
    .then((token) => {
      console.log(`FCM token`, token);
    });

  const unsubscribe = messaging().onMessage(async (remoteMessage) => {
    console.log('A new FCM message arrived!', JSON.stringify(remoteMessage));
    sendLocalNotification(remoteMessage);
  });

  return unsubscribe;

}, []);
```

So we just got remote notification from FCM using `messaging().onMessage()` and then we calling `Notifications.postLocalNotification()` that will trigger `NotificationReceivedForeground` event.

# Example 
To see this in the action and to check the whole code you can use [Sandbox-Mobile-App](https://github.com/uptechteam/Sandbox-Mobile-App), that we mentioned in [Deployment Pipeline](deployment-pipeline.md) section.

To send remote notification from Firebase check [this](https://rnfirebase.io/messaging/notifications#via-firebase-console)