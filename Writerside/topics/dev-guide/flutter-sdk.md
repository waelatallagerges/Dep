---
id: dev-guide-flutter-sdk
title: Flutter SDK
---

The DEP Meet Flutter SDK provides the same user experience as the DEP Meet app, in the form of a Flutter plugin so that you can embed and customize DEP Meet in your own Flutter app.

## Sample application using the Flutter

If you want to see how easy integrating the DEP Meet Flutter SDK into a Flutter application is, take a look at the<br/>
[sample applications repository](https://github.com/DEP/DEP-meet-sdk-samples#flutter).

## Installation

### Add dependency

Add the dependency from command-line
```bash
$ flutter pub add DEP_meet_flutter_sdk
```

The command above will add this to the `pubspec.yaml` file in your project (you can do this manually):
```yaml
dependencies:
    DEP_meet_flutter_sdk: ^0.1.7
```

### Install 

Install the packages from the terminal:

```bash
$ flutter pub get
```

### Import files

Import the following files into your dart code:

```dart
import 'package:DEP_meet_flutter_sdk/DEP_meet_flutter_sdk.dart';
```

### Usage

#### Join meeting

Firstly, create a `DEPMeet` object, then call the method `join` from it with a `DEPMeetConferenceOptions` object

```dart
var DEPMeet = DEPMeet();
var options = DEPMeetConferenceOptions(room: 'DEPIsAwesome');
DEPMeet.join(options);
```

## Configuration

### iOS

Make sure in `Podfile` from the `ios` directory you set the ios version `12.4 or higher` 

```
platform :ios, '12.4'
```

The plugin requests camera and microphone access, make sure to include the required entries for `NSCameraUsageDescription` and `NSMicrophoneUsageDescription` in your `Info.plist` file from the `ios/Runner` directory.

```
<key>NSCameraUsageDescription</key>
<string>The app needs access to your camera for meetings.</string>
<key>NSMicrophoneUsageDescription</key>
<string>The app needs access to your microphone for meetings.</string>
```

### Android

Go to `android/app/build.gradle` and make sure that the `minSdkVersion` is set to at least 24`

```
android {
    ...
    defaultConfig {
        ...
        minSdkVersion 24
    }
}
```


The `application:label` field from the DEP Meet Android SDK will conflict with your application's one . Go to `android/app/src/main/AndroidManifest.xml` and add the tools library and `tools:replace="android:label"` to the application tag.

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" 
    xmlns:tools="http://schemas.android.com/tools">
    <application
        tools:replace="android:label"
        android:label="sample_app"
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher">
        ...
    </application>
</manifest>
```
## Using the API

### DEPMeet

The `DEPMeet` class is the entry point for the SDK. It is used to launch the meeting screen and to send and receive all the events.

1. ####  DEPMeet()
    The constructor for the class.


2. ####  join(DEPMeetConferenceOptions options, [DEPMeetEventListener? listener])
    Joins a meeting with the given options and optionally a listener is given

    - `options` : meeting options
    - `listener` : event listener for events triggered by the native SDKs

3. #### hangUp()

    The localParticipant leaves the current meeting.

4. #### setAudioMuted(bool muted)

    Sets the state of the localParticipant audio muted according to the `muted` parameter.

5. #### setVideoMuted(bool muted)
    Sets the state of the localParticipant video muted according to the `muted` parameter.

6. #### sendEndpointTextMessage({String? to, required String message})
    Sends a message via the data channel to one particular participant or all of them. If the `to` param is empty, the message will be sent to all the participants in the conference.

    To get the participantId, the `participantsJoined` event should be listened for, which has as a parameter the `participantId` and this should be stored somehow.

7. #### toggleScreenShare(bool enabled)
    Sets the state of the localParticipant screen sharing according to the `enabled` parameter.

8. #### openChat([String? to])

    Opens the chat dialog. If `to` contains a valid participantId, the private chat with that particular participant will be opened.

9. #### sendChatMessage({String? to, required String message})

    Sends a chat message to one particular participant or all of them. If the `to` param is empty, the message will be sent to all the participants in the conference.

    To get the participantId, the `participantsJoined` event should be listened for, which has as a parameter the `participantId` and this should be stored somehow.

10. #### closeChat()

    Closes the chat dialog.

11. #### retrieveParticipantsInfo()

    Sends an event that will trigger the `participantsInfoRetrieved` event which will contain participants' information


### DEPMeetConferenceOptions

This object encapsulates all the options that can be tweaked when joining a conference.

Example:

```dart
var options = DEPMeetConferenceOptions(
      serverURL: "https://meet.jit.si",
      room: "DEPIsAwesomeWithFlutter",
      configOverrides: {
        "startWithAudioMuted": false,
        "startWithVideoMuted": false,
        "subject" : "DEP with Flutter",
      },
      featureFlags: {
        "unsaferoomwarning.enabled": false
      },
      userInfo: DEPMeetUserInfo(
          displayName: "Flutter user",
          email: "user@example.com"
      ),
    );
```

- All the values that can be added to the `configOverrides` can be found [here](https://github.com/DEP/DEP-meet/blob/master/config.js).

- All the values that can be added to the `featureFlags` can be found [here](https://github.com/DEP/DEP-meet/blob/master/react/features/base/flags/constants.ts).

- #### DEPMeetUserInfo({String displayName, String email, String avatar})
    The constructor for the DEPMeetUserInfo. 
P.S. the avatar should be an url.

### DEPMeetEventListener

This class intends to be used as a listener for events that come from the native sdks. It will receive as arguments the event handlers

1. #### conferenceJoined(String url)

    Called when a conference was joined.
    - `url` : the conference URL

2. #### conferenceTerminated(String url, Object? error)

    Called when the active conference ends, be it because of user choice or because of a failure.

    - `url` : the conference URL
    - `error` : missing if the conference finished gracefully, otherwise contains the error message

3. #### conferenceWillJoin(String url)

    Called before a conference is joined.

    - url: the conference URL

4. #### participantJoined(String? email, String? name, String? role, String? participantId) 

    Called when a participant has joined the conference.

    - `email` : the email of the participant. It may not be set if the remote participant didn't set one.
    - `name` : the name of the participant.
    - `role` : the role of the participant.
    - `participantId` : the id of the participant.

5. #### participantLeft(String? participantId)

    Called when a participant has left the conference.

    - `participantId` : the id of the participant that left.

6. #### audioMutedChanged(bool muted)

    Called when the local participant's audio is muted or unmuted. 

    - `muted` : a boolean indicating whether the audio is muted or not.

7. #### videoMutedChanged(bool muted)

    Called when the local participant's video is muted or unmuted. 

    - `muted` : a boolean indicating whether the video is muted or not.

8. #### endpointTextMessageReceived(String senderId, String message)

    Called when an endpoint text message is received.

    - `senderId` : the participantId of the sender
    - `message` : the content.

9. #### screenShareToggled(String participantId, bool sharing)

    Called when a participant starts or stops sharing his screen.

    - `participantId` : the id of the participant
    - `sharing` : the state of screen share

10. #### chatMessageReceived(String senderId, String message, bool isPrivate, String? timestamp)

    Called when a chat text message is received.

    - `senderId` : the ID of the participant that sent the message.
    - `message` : the content of the message.
    - `isPrivate` : true if the message is private, false otherwise.
    - `timestamp` : the (optional) timestamp of the message.

11. #### chatToggled(bool isOpen)

    Called when the chat dialog is opened or closed.

    - `isOpen` : true if the chat dialog is open, false otherwise.

12. #### participantsInfoRetrieved(String participantsInfo)
    Called when the `retrieveParticipantsInfo` action is called

    - `participantsInfo` : a list of participants' information as a string.

13. #### readyToClose()
    Called when the SDK is ready to be closed. No meeting is happening at this point.

#### Example of listener:

```dart
var listener = DEPMeetEventListener(
      conferenceJoined: (url) {
        debugPrint("conferenceJoined: url: $url");
      },

      participantJoined: (email, name, role, participantId) {
        debugPrint(
          "participantJoined: email: $email, name: $name, role: $role, "
              "participantId: $participantId",
        );
        participants.add(participantId!);
      },

      chatMessageReceived: (senderId, message, isPrivate) {
        debugPrint(
          "chatMessageReceived: senderId: $senderId, message: $message, "
              "isPrivate: $isPrivate",
        );
      },

      readyToClose: () {
        debugPrint("readyToClose");
      },
    );
```