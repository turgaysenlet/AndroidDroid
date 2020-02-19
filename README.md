# AndroidDroid
AndroidDroid - Android, Linux, ROS and Unity based robot code
## Overview

## Setup Steps
### Prerequisites
#### Hardware
* Google Pixel 1 phone - or any other Android phone, but the steps may differ
* USB-C data cable

### Become A Developer on Android Phone
* This is needed to do most of the operations and set some of the detailed settings on the phone
1. Click <b>Settings</b>
2. Click <b>System</b>
3. Click <b>About phone</b>
4. Click <b>Build number</b> <i>7 times</i>
5. May ask for your password, PIN or fingerprint
6. <b>Developer option</b> menu becomes available under Setting->System

### Enable USB Debugging on Android Phone
* This is needed to make phone communicate with the PC via USB cable, to build, debug apps and download upload files from the phone
1. First <b>Become A Developer</b>
2. Under Settings->System->Developer options click <b>USB debugging</b>

### Unlock Boot Loader on Android
* This is needed to load a new bootloader to the phone, mainly needed for rooting the phone
1. First <b>Become A Developer</b>
2. Under Settings->System->Developer options click <b>OEM unlocking</b> - this does not unlock, it only enables the next steps of fastboot unlock
3. May ask for your password, PIN or fingerprint
4. Use <b>adb</b> to restart in bootloader
```
$ adb reboot bootloader
```
5. Use <b>fastboot</b> to unlock boot loader
```
$ fastboot flashing unlock
```
Expected to see a message telling device is unlocked (or already unlocked)
6. Use <b>fastboot</b> to reboot back to Android OS
```
$ fastboot reboot
```
Now and every boot, expect to see a warning about bootloader cannot be verified for corruption, this is okay

### Install Android OS on the Phone
* This could be needed if you need to change the current version of the Android OS installed on your phone. Installing a version of Android that can easily be rooted is more important than the actual version number itself.
* I will be installing Android 8.1.0 Build <b>OPM1.171019.012</b>. This seems to be an up-to-date Android 8 and it should be fine since in previous attempts rooting Android 10 with Magisk did not work. 
1. Got to <b>Factory Images for Nexus and Pixel Devices</b> at https://developers.google.com/android/images
2. Download <b>8.1.0 (OPM1.171019.012, Jan 2018)</b> at https://dl.google.com/dl/android/aosp/sailfish-opm1.171019.012-factory-49ed1aec.zip

### Install Ubuntu OS on the Phone


## References
* For rooting, loosely following https://highonandroid.com/android-root/how-to-root-android-10-pixel-pixel-2-pixel-3-pixel-3a
