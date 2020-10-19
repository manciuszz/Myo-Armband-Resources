# Known Issues and Limitations

The following limitations will be resolved in future updates of the SDK:

*   The coordinate frame for orientation data is not currently specified.
*   Some firewall software (notably ESET NOD32) can block communication between the SDK and Myo Connect. Adding an exception in the firewall will resolve the issue.

**Known Issues with Myo Scripting**

*   myo.centerMousePosition() will always center to the primary monitor
*   MIDI support does not currently work on Windows.

# Release History

## Version 0.9.0

**Requirements**

*   Myo Connect version 0.14.0 or greater is required for the new events in this SDK release.

**Improvements**

*   A new event, [myo::DeviceListener::onBatteryLevelReceived()](classmyo_1_1_device_listener.html#ad29597d9acec7a1a9f1ae360f539f952 "Called when a paired Myo receives an battery level update. "), is called when the Myo's battery level changes and when the battery level is requested
*   A new [myo::Myo::requestBatteryLevel()](classmyo_1_1_myo.html#a7fb0194bf3c2f5b5bcd8064ac26832b1 "Request the battery level of the Myo. ") member function sends a battery level request to the myo.
*   Added new libmyo enums, `libmyo_warmup_state_t` and `libmyo_warmup_result_t`.
*   Added new libmyo functions, `libmyo_event_get_warmup_state` and `libmyo_event_get_warmup_result` to obtain warmup information.
*   Added new libmyo function, `libmyo_event_get_rotation_on_arm` to obtain rotation of Myo on arm.
*   Added `WarmupState` and `WarmupResult` enums to [myo::DeviceListener](classmyo_1_1_device_listener.html "A DeviceListener receives events about a Myo. ").
*   Added Myo rotation on arm and `WarmupState` parameters to [myo::DeviceListener](classmyo_1_1_device_listener.html "A DeviceListener receives events about a Myo. ") method `onArmSync`.
*   Added a new event, [myo::DeviceListener::onWarmupCompleted()](classmyo_1_1_device_listener.html#a8661d1a2e3a0813788fbbd70a3520256 "Called when the warmup period for a Myo has completed. "), which is called when the Myo has detected the end of warmup.
*   Added new script API, `myo.mouseScrollBy()`, which allows control over the mouse scrollwheel.
*   Added new script API, `myo.presentationPointer()`, which allows you to show or hide the presentation pointer.
*   Added new script API, `myo.presentationPointerEnabled()` and `myo.presentationPointerTailEnabled()` to determine the state of the pointer.
*   Added new script API, `myo.centerPresentationPointer()`, which centers the presentation pointer on the screen.
*   Added new script API, `myo.presentationPointerZoom()`, which allows you to zoom the screen to the presentation pointer.
*   Added new script API, `myo.presentationPointerZoomActive()` to determine the state of the full-screen zoom.

## Version 0.8.1

**Bug fixes**

*   Fixed missing Myo in `Hub - 2 Myos` Unity prefab.
*   Fixed setting of locking policy additional times.

**Myo Scripting Improvements - Myo Connect 0.8.1 required**

*   New mediaKey() function allows sending system media key events.
*   Mouse control is no longer bound to the primary display on OS X.

## Version 0.8.0

**Requirements**

*   Myo firmware version 1.1.5 or greater is required for streaming of EMG data without reducing performance of the gesture classifier. Only one Myo can stream EMG data reliably at a time.

**Improvements**

*   A new [myo::Myo::setStreamEmg()](classmyo_1_1_myo.html#a1aa96dbe82263c277dcfa6814ea22ab9 "Sets the EMG streaming mode for a Myo. ") member function allows enabling or disabling the streaming of EMG data.
*   A new event, [myo::DeviceListener::onEmgData()](classmyo_1_1_device_listener.html#a79f2abac09f0408c859cccf991d5294a "Called when a paired Myo has provided new EMG data. "), is called when a paired Myo has provided new EMG data when streaming is enabled.

**Myo Scripting Improvements**

*   The script reload button in the Myo Connect Application Manager has been restored. It will appear when in developer mode.
*   Myo scripts that can not be loaded (e.g. they have syntax errors) will no longer disappear from the Application Manager.
*   Myo Connect now persists the disabled state of scripts.
*   Myo scripts loaded in developer mode are no longer copied to the standard install location, and are reloaded from the original source location.

## Beta Release 7

**Requirements**

*   Myo firmware version 1.1.0 or greater.
*   Myo Connect version 0.7.0.

**Backwards compatibility notes**

*   The `doubleTap` pose has replaced the `thumbToPinky` pose. See [myo::Pose](classmyo_1_1_pose.html "A pose represents a detected configuration of the user's hand. ").
*   Myo now starts locked when it syncs, and only delivers poses when unlocked. This behavior can be changed by setting the locking policy.
*   The websocket API version has been changed to 3.

**Improvements**

*   A new myo::HubHub::setLockingPolicy() member function allows setting how a Myo's unlocked state affects poses.
*   A new [myo::Myo::notifyUserAction](classmyo_1_1_myo.html#ac54c392d495c2824149c0ff69cd63633 "Notify the Myo that a user action was recognized. ") member function allows triggering the standard Myo action vibration.
*   New [myo::Myo](classmyo_1_1_myo.html "Represents a Myo device with a specific MAC address. ") member functions, unlock() and lock(), allow controlling Myo's unlocked state.
*   New [myo::DeviceListener](classmyo_1_1_device_listener.html "A DeviceListener receives events about a Myo. ") events, `onUnlock` and `onLock`, are called when a Myo unlocks or locks.

**Myo Scripting Improvements**

*   Similarly to the main SDK, Myo scripting has been updated to include functions and events for the locking policy, triggering standard Myo actions, and locking state.
*   New API functions getAccel(), getAccelWorld(), getGyro(), midi(), and midiMachineControl() have been added.
*   The getRoll(), getYaw(), and getPitch() methods have been normalized to be related to a user's arm instead of the Myo orientation.
*   Myo scripts now include global variables scriptTitle and scriptDetailsUrl.
*   In onForegroundWindowChange, the app parameter on Windows will now be the executable filename.
*   The debug window is now off by default. To access it, enable developer mode in the Myo Connect Preferences.
*   Myo scripts with the file extension .myo will now be automatically added to the Myo application manager when launched.
*   The script reload button in the Myo Connect application manager has been removed due to instability. It may be readded at a later date.

## Beta Release 6

**Backwards compatibility notes**

*   Applications built with the SDK will only work with Myo Connect version 0.6.0.
*   libmyo_event_arm_recognized is now libmyo_event_arm_synced and libmyo_event_arm_lost is now libmyo_event_arm_unsynced.
*   onArmRecognized() is now onArmSync() and onArmLost() is now onArmUnsync().

**Improvements**

*   Myo armbands no longer lose their arm sync state when disconnecting.
*   Connecting to a synced Myo armband now triggers an arm synced event.
*   Disconnecting from a synced Myo armband now triggers an arm unsynced event.
*   The logo LED now pulses when the Myo armband is not synced, and becomes solid once synced.

## Beta Release 5

**Backwards compatibility notes**

*   Myo Connect's websocket server is communicating over port 10138 instead of 7204\. As a result, this version of the SDK is only compatible with Myo Connect version 0.5.0 or greater.

**Bug fixes**

*   Fixed crash in multiple-myos sample.
*   Fixed Visual Studio 2012 project files for samples.

## Beta Release 4

**Improvements**

*   Myo Connect now supports using multiple Myo armbands concurrently.
*   Myo armbands can now be managed in Myo Connect via the Manage Myo Armbands window.
*   Mouse control has been added to Myo Scripts! See the [Myo Script API Reference](script-reference.html#script-api-clickMouse) documentation for details.

## Beta Release 3

**Improvements**

*   Myo Scripts have been added to Myo Connect! See the [Writing Myo Scripts](script-tutorial.html) documentation for details.
*   A new event, [myo::DeviceListener::onUnpair()](classmyo_1_1_device_listener.html#afd9a510fbf547fa764a7e80f733b1081 "Called when a Myo has been unpaired. "), is called when the user disconnects from a Myo armband in Myo Connect.
*   Myo armbands can now be renamed through Myo Connect.
*   The pose window has been added under the Help menu in Myo Connect.

## Beta Release 2

**Improvements**

*   Added gesture data collection to Myo Connect. Help us improve Myo armband gesture recognition by recording your gesture data! You can access the gesture data collection from Myo Connect's menu.
*   Myo armbands can now be disconnected and reconnected through Myo Connect. Myo Connect will not automatically pair to disconnected Myo armbands on startup.
*   Myo Connect now starts automatically when you login. This can be disabled in Myo Connect Preferences.

**Bug fixes**

*   Events are now sent properly to applications for Myo armbands paired using USB.
*   Fixed an issue where Myo armbands would sometimes not be detected over USB.

## Beta Release 1

**Improvements**

*   Myo armbands no longer need to be trained! The trainer has been removed.
*   The `libmyo` library now connects to Myo armbands through the Myo Connect application, which allows multiple applications on the same computer to use Myo armbands at the same time.
*   A new event, myo::DeviceListener::onArmRecognized(), is called when a paired Myo armband detects it is on an arm. The event includes the detected arm (left or right) and the orientation of the Myo (positive x axis towards the wrist or the elbow).
*   A new event, myo::DeviceListener::onArmLost(), is called when a paired Myo armband detects it is moved/removed from an arm.
*   The SDK license has been replaced with a new license not exclusive to members of the Alpha program.

**Backwards compatibility notes**

*   The pairing functionality has moved from the SDK into Myo Connect. Functions such as `Hub::pairWithAnyMyo()` have been removed.
*   The `Hub::now()` member function has been removed.
*   Access to the MAC address of the Myo armband has been removed.
*   Application code that relies on gyroscope values should be revised to use the corrected values. Corrected values will be 16.384 times larger that before.
*   The `thumbToPinky` pose has replaced the `twistIn` pose. See [myo::Pose](classmyo_1_1_pose.html "A pose represents a detected configuration of the user's hand. ").
*   Myo's firmware version is now passed as a parameter in the [myo::DeviceListener::onConnect()](classmyo_1_1_device_listener.html#a29ab3696d66a787e296017ce74abcee9 "Called when a paired Myo has been connected. ") and [myo::DeviceListener::onPair()](classmyo_1_1_device_listener.html#af2b09ca659ea0a2f604117d1d49af2e1 "Called when a Myo has been paired. ") functions.

    In classes derived from [myo::DeviceListener](classmyo_1_1_device_listener.html "A DeviceListener receives events about a Myo. "), instead of writing:

    ```
    void onPair(myo::Myo* myo, uint64_t timestamp);

    void onConnect(myo::Myo* myo, uint64_t timestamp);
    ```

    you should now write:

    ```
    void onPair(myo::Myo* myo, uint64_t timestamp,
                myo::FirmwareVersion firmwareVersion);

    void onConnect(myo::Myo* myo, uint64_t timestamp,
                   myo::FirmwareVersion firmwareVersion);
    ```

**Bug fixes**

*   The scale of gyroscope values was corrected.

## Alpha Release 6

**Backwards compatibility notes**

*   The header include path for the C++ bindings has changed from `<myo.hpp>` to `<[myo/myo.hpp](_myo_8hpp_source.html)>`.

    Instead of writing:

    ```
    #include <myo.hpp>
    ```

    you should now write:

    ```
    #include <myo/myo.hpp>
    ```

*   The items of the [myo::Pose::Type](classmyo_1_1_pose.html#ae6566276cac4694db8e9e5873c5b0acf "Types of poses supported by the SDK. ") enum and the [myo::Myo::VibrationType](classmyo_1_1_myo.html#a13be9e9075fb3cf5d47ba491306f3271 "Types of vibration supported by the Myo. ") enum have been renamed using the lowerCamelCase convention.

    For example, instead of writing:

    ```
    if (pose == myo::Pose::wave_out)
    ```

    you should now write:

    ```
    if (pose == myo::Pose::waveOut)
    ```

**Improvements**

*   Mac OS X is now a supported platform.
*   The `rest` pose has replaced the `none` pose. See [myo::Pose](classmyo_1_1_pose.html "A pose represents a detected configuration of the user's hand. ").
*   The `unknown` pose has been added to indicate when Myo is not generating pose events. See [myo::Pose](classmyo_1_1_pose.html "A pose represents a detected configuration of the user's hand. ").
*   The new [rotate()](classmyo_1_1_quaternion.html#a23b8c84385a2486f37abd14a07ee6c65 "Return a copy of this vec rotated by quat. ") function allows using a quaternion to rotate a vector.
*   The new [myo::Quaternion::fromAxisAngle()](classmyo_1_1_quaternion.html#af4397481d462d3480b45708f38c1db77 "Return a quaternion that represents a right-handed rotation of angle radians about the given axis...") member function allows creating a quaternion from a given axis and angle of rotation.
*   The `ble32.dll` and `ble64.dll` libraries are no longer required or provided.
*   The `msvcr120.dll` and `msvcp120.dll` libraries are no longer required to use or distribute the SDK.
*   The MyoUnity.unitypackage is now included with the SDK and supports both Windows and Mac OS X.

## Alpha Release 5

**Bug fixes**

*   Multiple Myo armbands now classify poses correctly.

## Alpha Release 4

**Improvements**

*   When using updated firmware, a new pose recognition algorithm is enabled that provides more consistent recognition of poses.
*   The SDK now supports using multiple Myo armbands concurrently.
*   The new [myo::Myo::requestRssi()](classmyo_1_1_myo.html#a38477309f70709e2bf1d3d1a82d30e00 "Request the RSSI of the Myo. ") function allows retrieving Myo's signal strength, which will be delivered as a [myo::DeviceListener::onRssi()](classmyo_1_1_device_listener.html#a78c404fbd7649e11aed5c4d10705df74 "Called when a paired Myo has provided a new RSSI value. ") event.
*   The new myo::Myo::isTrained() function can be used to check whether a Myo is trained and will generate pose events.

**Bug fixes**

*   myo::Hub::waitForAnyMyo() no longer hangs when no argument is provided.
*   It is now safe to declare a static instance of [myo::Hub](classmyo_1_1_hub.html "A Hub provides access to one or more Myo instances. ").

## Alpha Release 3

**Backwards compatibility notes**

*   The Myo SDK now supports both 32 and 64 bit applications. Instead of linking to `myo.lib`, you should now link to `myo32.lib` or `myo64.lib` as appropriate. more information.

**Improvements**

*   The `twist_in` pose is now available.
*   A 32-bit build of the SDK is now available.
*   The [myo::DeviceListener::onOrientationData()](classmyo_1_1_device_listener.html#adaee14d3c4f9df61899ac8aa95b6bbc6 "Called when a paired Myo has provided new orientation data. ") event now provides normalized (i.e. unit length) quaternions.
*   A new pairing mode, adjacent pairing, provides the ability to pair with Myo only when it's very close to the Bluetooth antenna. See myo::Hub::waitForAdjacentMyo().
*   A new event, [myo::DeviceListener::onGyroscopeData()](classmyo_1_1_device_listener.html#ad9ac9d1d839804022c759b6f225a0032 "Called when a paired Myo has provided new gyroscope data in units of deg/s. "), provides angular velocity data.
*   Results of training are now associated with a specific Myo.
*   The new myo::Myo::macAddressAsString() function provides a string representation of Myo's MAC address.

## Alpha Release 2

**Improvements**

*   Accelerometer data is provided in units of g.
*   In the trainer, examples can now be skipped.
*   [myo::Vector3](classmyo_1_1_vector3.html "A vector of three components. ") now provides `x()`, `y()` and `z()` accessors.

**Bug fixes**

*   The trainer would sometimes not show recognized poses on "Try it" screen, even though training succeeded (especially on Windows 7).
*   When an application using the SDK shuts down, Myo would not disconnect right away.
*   In the trainer, results would be overwritten even when the Save and Close button was not clicked.

## Alpha Release 1

*   Initial release.