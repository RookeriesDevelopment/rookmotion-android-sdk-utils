# RookLink Utils

This SDK contains utility functions to help developers integrate our main SDK.

We use this functions in the following products:

* RookMotion Android App

## Contents

1. [Installation](#installation)
2. [NetworkManager](#network-manager)
    1. [StaticMethods](#network-manager-static-methods)
3. [BatteryManager](#battery-manager)
    1. [InstanceMethods](#battery-manager-instance-methods)
    2. [StaticMethods](#battery-manager-static-methods)
4. [BluetoothManager](#bluetooth-manager)
    1. [InstanceMethods](#bluetooth-manager-instance-methods)
    2. [StaticMethods](#bluetooth-manager-static-methods)
5. [LocationManager](#location-manager)
    1. [InstanceMethods](#location-manager-instance-methods)
    2. [StaticMethods](#location-manager-static-methods)
6. [PermissionsManager](#permissions-manager)
    1. [Constants](#permissions-manager-constants)
    2. [InstanceMethods](#permissions-manager-instance-methods)
    3. [StaticMethods](#permissions-manager-static-methods)
    
---

## Installation ##

### required software

To use this SDK the following steps are required

1. Add the following gradle configuration :

```groovy
android {
    compileSdkVersion 31

    defaultConfig {
        minSdkVersion 23
        targetSdkVersion 31
    }
}
```

2. Add the following permissions to your AndroidManifest.xml

```xml

<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.example.rookmotion">

    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

    <uses-permission android:name="android.permission.REQUEST_IGNORE_BATTERY_OPTIMIZATIONS"/>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

    <uses-permission
            android:name="android.permission.BLUETOOTH"
            android:maxSdkVersion="30"/>
    <uses-permission
            android:name="android.permission.BLUETOOTH_ADMIN"
            android:maxSdkVersion="30"/>

    <uses-permission
            android:name="android.permission.BLUETOOTH_SCAN"
            android:usesPermissionFlags="neverForLocation"
            tools:targetApi="s"/>

    <uses-permission android:name="android.permission.BLUETOOTH_CONNECT"/>
</manifest>
```

---

## Network Manager ##

Helper class to check network settings.

### Network Manager Static Methods ###

        canPingGoogle(timeout: Int): Boolean

Checks if device can connect to google. Executes on IO Dispatcher.

Parameters

* **timeout** Time limit to check connection, must be greater than 999.

Returns

* **Boolean** True if connection was successful, false if attempt fails or on timeout.


        isWifiEnabled(context: Context)

Checks if Wi-Fi state. This only checks Wi-Fi setting, not if the current Wi-Fi connection can reach internet.

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if device's Wi-Fi is enabled, false otherwise.


        isMobileDataEnabled(context: Context)

Checks if mobile data state. This only checks mobile data setting, not if the current mobile data connection can reach
internet.

This checks active network capabilities, if Wi-Fi is enabled this method will return false.

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if device's mobile data is enabled, false otherwise.


        isWifiOrMobileDataEnabled(context: Context)

Checks if Wi-Fi or mobile data state. This only checks Wi-Fi and mobile data setting, not if the current Wi-Fi or mobile
data connection can reach internet.

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if device's Wi-Fi or mobile data are enabled, false otherwise.

---

## Battery Manager ##

Helper class to manage battery settings.

### Battery Manager Instance Methods ###

        registerIgnoreOptimizationsListener(componentActivity: ComponentActivity, onSuccess: () -> Unit, onFailure: () -> Unit)

Registers a listener for battery optimizations requests.

This must only be called once. Recommended calling this method in your activity's onCreate method.

Parameters

* **componentActivity** ComponentActivity instance.
* **onSuccess** Callback when user allows the app to ignore battery optimizations.
* **onFailure** Callback when user denies the app from ignoring battery optimizations.


        registerIgnoreOptimizationsListener(fragment: Fragment, onSuccess: () -> Unit, onFailure: () -> Unit)

Registers a listener for battery optimizations requests.

This must only be called once. Recommended calling this method in your fragment's onCreateView method.

Parameters

* **fragment**  Fragment instance.
* **onSuccess** Callback when user allows the app to ignore battery optimizations.
* **onFailure** Callback when user denies the app from ignoring battery optimizations.


        requestIgnoreOptimizations(packageName: String)

Launches intent to ask user for disabling battery optimizations.

This will display a dialog over the application.

Parameters

* **packageName**  Application's package name


        onDestroy()

Unregisters all listeners and destroys all related instances.

Invoke this in your activity / fragment onDestroy method.

### Battery Manager Static Methods ###

        isIgnoringBatteryOptimizations(context: Context)

Checks current battery optimizations configuration.

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if your app is ignoring battery optimizations, false otherwise.

---

## Bluetooth Manager ##

Helper class to manage bluetooth settings.

### Bluetooth Manager Instance Methods ###

        registerEnableListener(componentActivity: ComponentActivity, onSuccess: () -> Unit, onFailure: () -> Unit)

Registers a listener for bluetooth requests.

This must only be called once. Recommended calling this method in your activity's onCreate method.

Parameters

* **componentActivity** ComponentActivity instance.
* **onSuccess** Callback when user turns on their bluetooth.
* **onFailure** Callback when user does not turn on their bluetooth.


        registerEnableListener(fragment: Fragment, onSuccess: () -> Unit, onFailure: () -> Unit)

Registers a listener for bluetooth requests.

This must only be called once. Recommended calling this method in your fragment's onCreateView method.

Parameters

* **fragment**  Fragment instance.
* **onSuccess** Callback when user turns on their bluetooth.
* **onFailure** Callback when user does not turn on their bluetooth.


        requestEnable()

Launches intent to ask user for turning on their bluetooth.

This will display a dialog over the application.

        onDestroy()

Unregisters all listeners and destroys all related instances.

Invoke this in your activity / fragment onDestroy method.

### Bluetooth Manager Static Methods ###

        isEnabled(context: Context)

Checks current bluetooth configuration.

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if bluetooth is on, false otherwise.

---

## Location Manager ##

Helper class to manage location settings.

### Location Manager Instance Methods ###

        registerEnableListener(componentActivity: ComponentActivity, onSuccess: () -> Unit, onFailure: () -> Unit)

Registers a listener for location requests.

This must only be called once. Recommended calling this method in your activity's onCreate method.

Parameters

* **componentActivity** ComponentActivity instance.
* **onSuccess** Callback when user turns on their location.
* **onFailure** Callback when user does not turn on their location.


        registerEnableListener(fragment: Fragment, onSuccess: () -> Unit, onFailure: () -> Unit)

Registers a listener for location requests.

This must only be called once. Recommended calling this method in your fragment's onCreateView method.

Parameters

* **fragment**  Fragment instance.
* **onSuccess** Callback when user turns on their location.
* **onFailure** Callback when user does not turn on their location.


        requestEnable()

Launches intent to ask user for turning on their location.

This will open the settings view of the application.

        onDestroy()

Unregisters all listeners and destroys all related instances.

Invoke this in your activity / fragment onDestroy method.

### Location Manager Static Methods ###

        isEnabled(context: Context)

Checks current location configuration.

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if location is on, false otherwise.

---

## Permissions Manager ##

Helper class to manage app permissions.

### Permissions Manager Constants ###

        locationPermissions

Array of the permissions grouped as locationPermissions, permissions included:

* Manifest.permission.ACCESS_FINE_LOCATION
* Manifest.permission.ACCESS_COARSE_LOCATION


        bluetoothPermissions

Array of the permissions grouped as locationPermissions, permissions included:

For Android 11 or lower:

* Manifest.permission.BLUETOOTH
* Manifest.permission.BLUETOOTH_ADMIN

For Android 12+:

* Manifest.permission.BLUETOOTH_SCAN
* Manifest.permission.BLUETOOTH_CONNECT

### Permissions Manager Instance Methods ###

        registerLocationPermissionsListener(componentActivity: ComponentActivity, onAllowed: (permissions: Map<String, Boolean>) -> Unit, onDenied: (permissions: Map<String, Boolean>) -> Unit)

Registers a listener for location permissions requests.

This must only be called once. Recommended calling this method in your activity's onCreate method.

Parameters

* **componentActivity** ComponentActivity instance.
* **onAllowed** Callback when grants all permissions.
* **onDenied** Callback when denies all or at least one permission.


        registerLocationPermissionsListener(fragment: Fragment, onAllowed: (permissions: Map<String, Boolean>) -> Unit, onDenied: (permissions: Map<String, Boolean>) -> Unit)

Registers a listener for location permissions requests.

This must only be called once. Recommended calling this method in your fragment's onCreateView method.

Parameters

* **fragment**  Fragment instance.
* **onAllowed** Callback when grants all permissions.
* **onDenied** Callback when denies all or at least one permission.


        requestLocationPermissions()

Launches intent to ask user for location permissions, see [locationPermissions](#permissions-manager-constants).

This will open a permissions' dialog for each permission requested.

        registerBluetoothPermissionsListener(componentActivity: ComponentActivity, onAllowed: (permissions: Map<String, Boolean>) -> Unit, onDenied: (permissions: Map<String, Boolean>) -> Unit)

Registers a listener for bluetooth permissions requests.

This must only be called once. Recommended calling this method in your activity's onCreate method.

Parameters

* **componentActivity** ComponentActivity instance.
* **onAllowed** Callback when grants all permissions.
* **onDenied** Callback when denies all or at least one permission.


        registerBluetoothPermissionsListener(fragment: Fragment, onAllowed: (permissions: Map<String, Boolean>) -> Unit, onDenied: (permissions: Map<String, Boolean>) -> Unit)

Registers a listener for bluetooth permissions requests.

This must only be called once. Recommended calling this method in your fragment's onCreateView method.

Parameters

* **fragment**  Fragment instance.
* **onAllowed** Callback when grants all permissions.
* **onDenied** Callback when denies all or at least one permission.


        requestBluetoothPermissions()

Launches intent to ask user for bluetooth permissions, see [bluetoothPermissions](#permissions-manager-constants).

This will open a permissions' dialog for each permission requested.

        onDestroy()

Unregisters all listeners and destroys all related instances.

Invoke this in your activity / fragment onDestroy method.

### Permissions Manager Static Methods ###

        hasLocationPermissions(context: Context)

Checks location permissions, see [locationPermissions](#permissions-manager-constants).

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if all location permissions are granted, false otherwise.


        hasBluetoothPermissions(context: Context)

Checks bluetooth permissions, see [bluetoothPermissions](#permissions-manager-constants).

Parameters

* **context** Application, activity or fragment context.

Returns

* **Boolean** True if all bluetooth permissions are granted, false otherwise.
