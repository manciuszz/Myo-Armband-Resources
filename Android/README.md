# Known Issues and Limitations

The following limitations will be resolved in future updates of the SDK:

*   The coordinate frame for orientation data is not currently specified.
*   Two apps cannot concurrently use the Myo on the same device.

# Release History

## Version 0.10.0

**Improvements**

*   Added `getArm()`, `getXDirection()`, `getPose()` to `Myo` for returning the current Myo state.

**Bug fixes**

*   Fixed an issue that could prevent Bluetooth from being turned off after disconnecting a Myo from a Lollipop device.

## Beta Release 4

**Requirements**

*   Myo firmware version 1.1.0 or greater.

**Backwards compatibility notes**

*   The `THUMB_TO_PINKY` pose has been replaced by `DOUBLE_TAP`.
*   Myo now starts locked when it syncs, and only delivers poses when unlocked. This behavior can be changed by setting the locking policy.
*   Apps that use multiple Myo armbands must now specify the maximum number of attached Myos. This should be done after initializing the Hub. See `Hub.setMyoAttachAllowance()`. If unspecified, this value defaults to 1.
*   The Myo Android SDK now requires Android API Level 18 or higher.

**Improvements**

*   A new method, `Hub.setLockingPolicy()`, allows setting how a Myo's unlocked state affects poses.
*   A new method, `Myo.notifyUserAction()`, allows triggering the standard Myo action vibration.
*   New `Myo` methods, `unlock(UnlockType)` and `lock()`, allow controlling Myo's unlocked state.
*   New `DeviceListener` methods, `onUnlock` and `onLock`, are called when a Myo unlocks or locks.
*   A new method, `Hub.setMyoAttachAllowance()`, allows you to set the maximum number of Myo armbands that are allowed to simultaneously be attached to.
*   If Bluetooth is disabled when a list item or the Scan option item is clicked in the ScanActivity or ScanFragment, a dialog prompting the user to enable Bluetooth will pop up.
*   Fixed issue that caused all scanned Myos to appear as "Unknown Myo" in the ScanFragment.

## Beta Release 3

**Requirements**

*   Myo firmware version 1.0.0 or greater.

**Backwards compatibility notes**

*   The DeviceListener method `onPair()` has been renamed to `onAttach()`.
*   The Hub methods `pairWithAdjacentMyo()` and `pairByMacAddress()` have been renamed to `attachToAdjacentMyo()` and `attachByMacAddress()`.
*   The Hub methods `pairWithAnyMyo` and `pairWithAnyMyos` have been removed. The ScanActivity or the `attachToAdjacentMyo` and `attachToAdjacentMyos` methods should be used instead.
*   `onArmRecognized()` is now `onArmSync()` and `onArmLost()` is now `onArmUnsync()`.

**Improvements**

*   Removed `READ_EXTERNAL_STORAGE` and `WRITE_EXTERNAL_STORAGE` permissions.
*   A new DeviceListener event, `onDetach()`, is called when an attached Myo armband becomes detached.
*   Myo armbands no longer lose their arm sync state when disconnecting.
*   Connecting to a synced Myo armband now triggers an arm synced event.
*   Disconnecting from a synced Myo armband now triggers an arm unsynced event.
*   The logo LED now pulses when the Myo armband is not synced, and becomes solid once synced.

## Beta Release 2

**Improvements**

*   A new sample app, called `Glass`, shows how to use Myo directly with Google Glass.
*   A new method, `Hub.unpair()`, allows disconnecting from a Myo. Previously this was only possible through the ScanActivity.

## Beta Release 1

**Improvements**

*   Myo armbands no longer need to be trained! The trainer has been removed.
*   Sending of usage data can be disabled. See `Hub.setSendUsageData()`.

## Alpha Release 4

**Backwards compatibility notes**

*   The Pose.Type enum has been removed, with Pose itself now being an enum instead.

    Instead of writing:

    ```
    if (pose.getType() == Pose.Type.Fist)
    ```

    you should now write:

    ```
    if (pose == Pose.Fist)
    ```

*   The `THUMB_TO_PINKY` pose has replaced the `TWIST_IN` pose.

**Improvements**

*   A new event, `onArmRecognized()`, is called when a paired Myo armband detects it is on an arm.
*   A new event, `onArmLost()`, is called when a paired Myo armband detects it is moved/removed from an arm.
*   An application identifier can now be specified in `Hub.init()`. See `Hub.init()` for the proper format.

## Alpha Release 3

**Improvements**

*   The `REST` pose has replaced the `NONE` pose.
*   The `UNKNOWN` pose has been added to indicate when Myo is not generating pose events.

## Alpha Release 2

**Bug fixes**

*   Multiple Myo armbands now classify poses correctly.
*   Listeners are now cleared when the Hub is shutdown.

## Alpha Release 1

*   Initial release.