# RookLink Utils

This SDK contains utility functions to help developers integrate our main SDK.

We use this functions in the following products:

* RookMotion Android App

---

## Contents

1. [Prerequisites](#prerequisites)
2. [Install](#install)
3. [Docs](#docs)

---

## Prerequisites

**IDE & Tools**

* Android Studio Chipmunk | 2021.2.1.
* Kotlin 1.6.10.
* Android Device or Emulator with BLE capabilities and Android 6+ (sdk 23).

**Android SDK**

Go to your **build.gradle** (app level) and apply the following configuration.

```groovy
android {
    compileSdk 31

    defaultConfig {
        minSdk 23
        targetSdk 31

        // Other configurations
    }

    // More configurations
}
```

**Android Permissions**

Go to your **AndroidManifest.xml** and apply the following permissions.

```xml

<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:tools="http://schemas.android.com/tools"
          package="com.rookmotion.rooktraining">

    <uses-permission android:name="android.permission.INTERNET"/>

    <!-- Check internet and battery settings -->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.REQUEST_IGNORE_BATTERY_OPTIMIZATIONS"/>

    <!-- Scan BLE peripherals -->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

    <!-- Android 6+ (sdk 23) bluetooth permissions-->
    <uses-permission
            android:name="android.permission.BLUETOOTH"
            android:maxSdkVersion="30"/>
    <uses-permission
            android:name="android.permission.BLUETOOTH_ADMIN"
            android:maxSdkVersion="30"/>

    <!-- Android 12+ (sdk 31) bluetooth permissions-->
    <uses-permission
            android:name="android.permission.BLUETOOTH_SCAN"
            android:usesPermissionFlags="neverForLocation"
            tools:targetApi="s"/>
    <uses-permission android:name="android.permission.BLUETOOTH_CONNECT"/>

    <!-- Other configurations -->
</manifest>
```

---

## Install

**Versioning**

This SDK uses Semantic Versioning: major.minor.patch.

Incompatible changes increment major version, adding compatible changes increment minor version, and compatible fixes
increment the patch version.

Each time a major release it made we'll provide you with a migration guide.

**Install from maven central**

Go to your **build.gradle** (app level) and declare the **sdk-utils** dependency, then sync your project.

* You can find the latest versions at [maven central](https://central.sonatype.dev/search?q=com.rookmotion.android).

```groovy
dependencies {

    // RookMotion
    implementation 'com.rookmotion.android:sdk-utils:$u_latest_version'

    // Other dependencies
}
```

* **sdk-utils** includes joda-time library, version 2.10.6 as a compile dependency.

---

## Docs

To explore the included classes go to
our [Javadoc](https://www.javadoc.io/doc/com.rookmotion.android/sdk-utils/latest/index.html)
