# Known Issues and Limitations

The following limitations will be resolved in future updates of the SDK:

*   The coordinate frame for orientation data is currently not specified.
*   The coordinate frame for accelerometer data and gyroscope data is currently not specified.
*   Myo Armbands can only be connected to a single app.
*   iOS devices sometimes have issues discovering services, causing a Myo connection to fail. This can be temporarily avoided by restarting the iOS device.

The following are iOS known issues and limitations.

*   On 64-bit iOS 7.0.x devices, bluetooth notification bandwidth is limited to 33.33 Hz, which may affect orientation streaming and pose recognition. This iOS bug is fixed in iOS 7.1.
*   If you do not enable background mode, you may see the following warning:

    ```
    CoreBluetooth[API MISUSE] <CBCentralManager: 0x145715b0> has no restore identifier but the delegate implements the centralManager:willRestoreState: method. Restoring will not be supported
    ```

    This warning is harmless and can be ignored.

# Release History

**Version 0.5.2**

Improvements:

*   Added [TLMMyo](interface_t_l_m_myo.html) object to relevant [TLMHub](interface_t_l_m_hub.html) notifications' userInfo dictionary. [TLMMyo](interface_t_l_m_myo.html) can be accessed using `kTLMKeyMyo` key.

**Version 0.5.1**

Improvements:

*   Added IBInspectable `showDoneButton` property to `[TLMSettingsViewController](interface_t_l_m_settings_view_controller.html)`.

Bug Fixes:

*   Fixed an issue where the scan button would not appear when using `[TLMSettingsViewController](interface_t_l_m_settings_view_controller.html)` in a storyboard.

**Version 0.5.0**

Requirements:

*   Myo firmware version 1.1.5 or greater is required for streaming of EMG data without reducing performance of the gesture classifier.

Improvements:

*   Added `[TLMEmgEvent](interface_t_l_m_emg_event.html)` event to [TLMMyo](interface_t_l_m_myo.html).
*   Added `- (void)setStreamEmg:(TLMStreamEmgType)type` method to [TLMMyo](interface_t_l_m_myo.html).

Bug Fixes:

*   Fixed a forward compatibility issue with Myo firmware. Applications should update to use this SDK as soon as possible.
*   Added missing myo and timestamp properties to `[TLMUnlockEvent](interface_t_l_m_unlock_event.html)` and `[TLMLockEvent](interface_t_l_m_lock_event.html)`.

**Version 0.4.0**

Breaking Changes:

*   Removed dependence on GLKit in order to better support Swift. GLKVector3 is replaced with TLMVector3, and GLKQuaternion is replaced with TLMQuaternion.

**Beta Release 3**

Requirements:

*   Myo firmware version 1.1.0 or greater.

Improvements:

*   Added `lockingPolicy` property to [TLMHub](interface_t_l_m_hub.html).
*   Added `- (void)unlockWithType:(TLMUnlockType)type` and `- (void)lock` methods to [TLMMyo](interface_t_l_m_myo.html).
*   Added `[TLMUnlockEvent](interface_t_l_m_unlock_event.html)` and `[TLMLockEvent](interface_t_l_m_lock_event.html)`.
*   Added `- (void)indicateUserAction` method on [TLMMyo](interface_t_l_m_myo.html).
*   Added `TLMPoseTypeDoubleTap`.

Breaking Changes:

*   Removed Thumb to Pinky pose.

**Beta Release 2**

Requirements:

*   Myo firmware version 1.0.0 or greater.

Improvements:

*   Added `pose` property to `[TLMMyo](interface_t_l_m_myo.html)`.
*   Added `orientation` property to `[TLMMyo](interface_t_l_m_myo.html)`.
*   Added `arm` and `xDirection` properties to `[TLMMyo](interface_t_l_m_myo.html)`.
*   Added `TLMArmUnknown` to `TLMArm` enum.
*   Added `TLMArmXDirectionUnknown` to `TLMArmXDirection` enum.
*   Myo armbands no longer lose their arm sync state when disconnecting.
*   Connecting to a synced Myo armband now triggers an arm synced event.
*   Disconnecting from a synced Myo armband now triggers an arm unsynced event.
*   The logo LED now pulses when the Myo armband is not synced, and becomes solid once synced.

Breaking Changes:

*   Removed `[TLMHub](interface_t_l_m_hub.html)`'s `attachToAny` method.
*   Changed `[TLMMyo](interface_t_l_m_myo.html)`'s `TLMArmRecognizedEvent` to `[TLMArmSyncEvent](interface_t_l_m_arm_sync_event.html)`. Related keys and notifications have been updated as well.
*   Changed `[TLMMyo](interface_t_l_m_myo.html)`'s `TLMArmLostEvent` to `[TLMArmUnsyncEvent](interface_t_l_m_arm_unsync_event.html)`. Related keys and notifications have been updated as well.

**Beta Release 1**

Improvements:

*   Added background support for Myo events.
*   Added new attaching and detaching methods. Attaching to a `[TLMMyo](interface_t_l_m_myo.html)` means the `[TLMHub](interface_t_l_m_hub.html)` will always try to maintain the connection to the Myo, even when the Myo disconnects.
*   Added ability to attach to a Myo by its identifier.
*   Supports trainingless pose classification.

Requirements:

*   Myo firmware version 0.8.11 or greater.

Breaking Changes:

*   Dropped support for iOS 6.
*   A single Myo Armband can no longer connect to multiple apps.
*   Changed `[TLMMyo](interface_t_l_m_myo.html)`'s property identifier from an NSString to an NSUUID. The NSString form can still be accessed like so:

    ```
    NSString *uuidString = myo.identifier.UUIDString;
    ```

*   Changed `[TLMHub](interface_t_l_m_hub.html)`'s `pairWithAdjacent` and `pairWithAny` to `attachToAdjacent` and `attachToAny`. You no longer need to stop `attachToAdjacent`, since it stops once a Myo is attached.
*   Removed training related methods. Myo no longer needs to be trained.

**Alpha Release 7**

Improvements:

*   The `TLMPoseTypeRest` pose has replaced the `TLMPoseTypeNone` pose.
*   The `TLMPoseTypeThumbToPinky` pose has replaced the `TLMPoseTypeTwistIn` pose.
*   The `TLMPoseTypeUnknown` pose has been added.
*   An applicationIdentifier property has been added to [TLMHub](interface_t_l_m_hub.html).

**Alpha Release 6**

Improvements:

*   Proper pose classification for multiple Myo armbands.

**Alpha Release 5**

Improvements:

*   New pose recognition algorithm which provides more consistent recognition of poses.
*   Support for multiple Myo armbands concurrently.

Requirements:

*   Myo firmware version 0.7.x.

Bug Fixes:

*   Issue parsing different firmware versions.

**Alpha Release 4**

Improvements:

*   arm64 and x86_64 support.

Breaking Changes:

*   Removed notificationDispatchQueue. If you want to receive notifications on a thread other than the main thread, use the NSNotificationCenter addObserverForName:object:queue:usingBlock: method.
*   Renamed TLMAccelerometerEvent.accelerationVector to [TLMAccelerometerEvent.vector](interface_t_l_m_accelerometer_event.html#a432258da57c8b280c7a942d3b9f8eb4a), TLMGyroscopeEvent.rotationRateVector to [TLMGyroscopeEvent.vector](interface_t_l_m_gyroscope_event.html#a35b35fbacb2444d8cde983b5c66003ac).

Bug Fixes:

*   Issue where training data was no longer being persisted.
*   Issue with receiving pose notifications while training.
*   Issue filtering out non-Myo BLE devices.
*   Assertion failure on creation of [TLMHub](interface_t_l_m_hub.html).

**Alpha Release 3**

Improvements:

*   Added Twist In pose.
*   Removed vibrate upon connection.
*   Added pairWithAdjacent pairing method.
*   Added gyroscope events.
*   Added [TLMHub](interface_t_l_m_hub.html) property to specify which dispatch queue to receive notifications on.

Bug Fixes:

*   An intermittent crash when a Myo disconnects during training.

**Alpha Release 2**

Improvements:

*   In the trainer, examples can now be skipped.
*   Several lower level optimizations involving Myo Bluetooth communication.

Bug Fixes:

*   A rare bug involving the storage of favourite devices was fixed.

**Alpha Release 1**

*   Initial release.