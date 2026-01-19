# community-cordova-plugin-firebase-analytics

Community maintained Cordova plugin for [Firebase Analytics](https://firebase.google.com/docs/analytics/).

[![NPM version](https://img.shields.io/npm/v/community-cordova-plugin-firebase-analytics.svg)](https://www.npmjs.com/package/community-cordova-plugin-firebase-analytics)
[![Downloads](https://img.shields.io/npm/dm/community-cordova-plugin-firebase-analytics)](https://www.npmjs.com/package/community-cordova-plugin-firebase-analytics)

## Support This Plugin

I dedicate a considerable amount of my free time to developing and maintaining many Cordova plugins for the community ([See the list with all my maintained plugins][community_plugins]).

To help ensure this plugin is kept updated, new features are added and bugfixes are implemented quickly, please donate a couple of dollars (or a little more if you can stretch) as this will help me to afford to dedicate time to its maintenance.

Please consider donating if you're using this plugin in an app that makes you money, or if you're asking for new features or priority bug fixes. Thank you!

[![Sponsor Me](https://img.shields.io/static/v1?label=Sponsor%20Me&style=for-the-badge&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)](https://github.com/sponsors/EYALIN)

## Credits & Acknowledgments

This plugin was originally forked from [cordova-plugin-firebase-analytics](https://github.com/chemerisuk/cordova-plugin-firebase-analytics) by [Maksim Chemerisuk](https://github.com/chemerisuk).

A huge thank you to the original author for creating and maintaining the original plugin. The original work laid the foundation for this plugin, and we are grateful for their contributions to the Cordova community.

Due to the original plugin no longer being actively maintained, this standalone repository was created to continue development, provide updates, and ensure compatibility with the latest Firebase SDK versions.

## Related Community Plugins

This plugin is part of a larger ecosystem of community-maintained Cordova plugins:

| Plugin | Description |
|--------|-------------|
| [community-cordova-plugin-firebase-crashlytics](https://github.com/EYALIN/community-cordova-plugin-firebase-crashlytics) | Firebase Crashlytics |
| [community-cordova-plugin-admob](https://github.com/EYALIN/community-cordova-plugin-admob) | Google AdMob |
| [community-cordova-plugin-consent](https://github.com/EYALIN/community-cordova-plugin-consent) | Google UMP Consent |

[View all community plugins][community_plugins]

## Index

<!-- MarkdownTOC levels="2,3" autolink="true" -->

- [Supported Platforms](#supported-platforms)
- [Installation](#installation)
- [SDK Versions](#sdk-versions)
- [Variables](#variables)
- [Disabling analytics data collection](#disabling-analytics-data-collection)
- [Disabling automatic screen collection](#disabling-automatic-screen-collection)
- [Adding required configuration files](#adding-required-configuration-files)
- [Functions](#functions)

<!-- /MarkdownTOC -->

## Supported Platforms

- iOS
- Android

## Installation

```bash
cordova plugin add community-cordova-plugin-firebase-analytics
```

If you get an error about CocoaPods being unable to find compatible versions, run:

```bash
pod repo update
```

Use variables `ANDROID_FIREBASE_BOM_VERSION` or `IOS_FIREBASE_POD_VERSION` to override dependency versions for Firebase SDKs:

```bash
cordova plugin add community-cordova-plugin-firebase-analytics \
    --variable IOS_FIREBASE_POD_VERSION="11.12.0" \
    --variable ANDROID_FIREBASE_BOM_VERSION="33.8.0"
```

NOTE: on iOS in order to collect demographic, age, gender data etc. you should additionally [include `AdSupport.framework`](https://firebase.google.com/support/guides/analytics-adsupport) into your project.

## SDK Versions

| Platform | SDK | Default Version |
|----------|-----|-----------------|
| Android | Firebase BOM | 33.8.0 |
| iOS | Firebase CocoaPods | 11.12.0 |

## Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `ANALYTICS_COLLECTION_ENABLED` | `true` | Enable/disable analytics collection on startup |
| `AUTOMATIC_SCREEN_REPORTING_ENABLED` | `true` | Enable/disable automatic screen reporting |
| `ANDROID_FIREBASE_BOM_VERSION` | `33.8.0` | Firebase BOM version for Android |
| `IOS_FIREBASE_POD_VERSION` | `11.12.0` | Firebase pod version for iOS |

## Disabling analytics data collection

In some cases, you may wish to temporarily or permanently disable collection of Analytics data. You can set the value of variable `ANALYTICS_COLLECTION_ENABLED` to `false` to prevent collecting any user data:

```bash
cordova plugin add community-cordova-plugin-firebase-analytics \
    --variable ANALYTICS_COLLECTION_ENABLED=false
```

Later you can re-enable analytics data collection (for instance after getting end-user consent) using method [setEnabled](#setenabledenabled).

## Disabling automatic screen collection

In order to [disable automatic collection of screen view events](https://firebase.googleblog.com/2020/08/google-analytics-manual-screen-view.html) set the value of variable `AUTOMATIC_SCREEN_REPORTING_ENABLED` to `false`:

```bash
cordova plugin add community-cordova-plugin-firebase-analytics \
    --variable AUTOMATIC_SCREEN_REPORTING_ENABLED=false
```

## Adding required configuration files

Cordova supports `resource-file` tag for easy copying resources files. Firebase SDK requires `google-services.json` on Android and `GoogleService-Info.plist` on iOS platforms.

1. Put `google-services.json` and/or `GoogleService-Info.plist` into the root directory of your Cordova project
2. Add new tag for Android platform

```xml
<platform name="android">
    ...
    <resource-file src="google-services.json" target="app/google-services.json" />
</platform>
...
<platform name="ios">
    ...
    <resource-file src="GoogleService-Info.plist" />
</platform>
```

This way config files will be copied on `cordova prepare` step.

## Functions

### logEvent

**logEvent**(`name`, `params`): `Promise`<`void`\>

Logs an app event.

**Example**

```ts
cordova.plugins.firebase.analytics.logEvent("my_event", {param1: "value1"});
```

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `name` | `string` | Event name |
| `params` | `Record`<`string`, `string` \| `number` \| `object`[]\> | Event parameters |

#### Returns

`Promise`<`void`\>

Callback when operation is completed

---

### resetAnalyticsData

**resetAnalyticsData**(): `Promise`<`void`\>

Clears all analytics data for this instance from the device and resets the app instance ID.

**Example**

```ts
cordova.plugins.firebase.analytics.resetAnalyticsData();
```

#### Returns

`Promise`<`void`\>

Callback when operation is completed

---

### setCurrentScreen

**setCurrentScreen**(`screenName`): `Promise`<`void`\>

Sets the current screen name, which specifies the current visual context in your app. This helps identify the areas in your app where users spend their time and how they interact with your app.

**Example**

```ts
cordova.plugins.firebase.analytics.setCurrentScreen("User dashboard");
```

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `screenName` | `string` | Current screen name |

#### Returns

`Promise`<`void`\>

Callback when operation is completed

---

### setDefaultEventParameters

**setDefaultEventParameters**(`defaults`): `Promise`<`void`\>

Adds parameters that will be set on every event logged from the SDK, including automatic ones.

**Example**

```ts
cordova.plugins.firebase.analytics.setDefaultEventParameters({foo: "bar"});
```

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `defaults` | `Record`<`string`, `string` \| `number` \| `object`[]\> | Key-value default parameters map |

#### Returns

`Promise`<`void`\>

Callback when operation is completed

---

### setEnabled

**setEnabled**(`enabled`): `Promise`<`void`\>

Sets whether analytics collection is enabled for this app on this device.

**Example**

```ts
cordova.plugins.firebase.analytics.setEnabled(false);
```

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `enabled` | `boolean` | Flag that specifies new state |

#### Returns

`Promise`<`void`\>

Callback when operation is completed

---

### setUserId

**setUserId**(`userId`): `Promise`<`void`\>

Sets the user ID property. This feature must be used in accordance with Google's Privacy Policy.

**See**

https://www.google.com/policies/privacy

**Example**

```ts
cordova.plugins.firebase.analytics.setUserId("12345");
```

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `userId` | `string` | User's identifier string |

#### Returns

`Promise`<`void`\>

Callback when operation is completed

---

### setUserProperty

**setUserProperty**(`name`, `value`): `Promise`<`void`\>

Sets a user property to a given value. Be aware of automatically collected user properties.

**See**

https://support.google.com/firebase/answer/6317486?hl=en&ref_topic=6317484

**Example**

```ts
cordova.plugins.firebase.analytics.setUserProperty("name1", "value1");
```

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `name` | `string` | Property name |
| `value` | `string` | Property value |

#### Returns

`Promise`<`void`\>

Callback when operation is completed

## Contributing

- Star this repository
- Open issue for feature requests
- [Sponsor this project](https://github.com/sponsors/EYALIN)

## License

MIT

[community_plugins]: https://github.com/EYALIN?tab=repositories&q=community&type=&language=&sort=
