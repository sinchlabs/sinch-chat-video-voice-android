

# Sinch Android RTC Plugin SDK - Getting Started



This is documentation how to easily implement RTC Plugin for Sinch Chat.



# Requirements



- Android 5.0 Lollipop - min SDK 21



# Installation



### Maven



settings.gradle

```

maven {
	url "https://raw.githubusercontent.com/sinchlabs/sinch-chat-video-voice-android/master/releases"
	credentials(HttpHeaderCredentials) {
	  name = "Authorization"
	  value = "Bearer {{ github_personal_access_token }}"
	}
	authentication {
	  header(HttpHeaderAuthentication)
	}
}
flatDir { dirs 'libs' }

```


1. Copy libs directory to your root project directory

build.gradle

```

implementation(name:'sinch-android-rtc', version:'+', ext:'aar')
implementation 'com.sinch.sdk.rtc.plugin:sinch-sdk-rtc-plugin:{version}'

```



# First steps



1. Setup Sinch Chat SDK
2. Copy `libs` directory from repo to your root project directory.
3. Add Sinch RTC Plugin as option in Sinch Chat SDK initialization method. (you can find example below)
4. Show chat

## Initialize



Call method `initialize` with `SinchInitializationOptions` and `plugins` property.



```swift

val options = SinchInitializationOptions(null)

val sinchRTCPlugin = SinchVideoRTCPluginSDK(
	{
		return@SinchVideoRTCPluginSDK this
	},
	  APPLICATION_KEY,
	  APPLICATION_SECRET,
		FCM_SENDER_ID
)
options.plugins = listOf(sinchRTCPlugin)
SinchChatSDK.initialize(this, options)
```


#### Troubleshooting

You may found issue with building your application. It is related to dependencies which we're using which are related to Protobuf.

Paste those lines in your android {} in build.gradle.


```
android {
    ...

    configurations {
        implementation.exclude module:'protolite-well-known-types'
        implementation.exclude module:'protobuf-lite'
    }
}

```
