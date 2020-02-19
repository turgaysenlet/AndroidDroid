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
* Unlocked bootloader is required
1. Got to <b>Factory Images for Nexus and Pixel Devices</b> at https://developers.google.com/android/images
2. Download <b>8.1.0 (OPM1.171019.012, Jan 2018)</b> at https://dl.google.com/dl/android/aosp/sailfish-opm1.171019.012-factory-49ed1aec.zip 
3. Even if you are not going to reinstall your Android OS, downloading the image is necessary for other steps of rooting
4. Unzip the downloaded file 
At this point you can follow the flashing instructions in https://developers.google.com/android/images#instructions, which are also listed below
5. Make sure you are a developer
6. Make sure you have enabled USB debugging
7. Make sure bootloader is unlocked
8. Use <b>adb</b> to restart in bootloader
```
$ adb reboot bootloader
```
9. Go to the unzipped image folder (exact path may differ)
```
$ cd ~/Downloads/sailfish-opm1.171019.012-factory-49ed1aec/sailfish-opm1.171019.012
```
10. Run <b>flash-all</b> script to do the install/falsh of the new OS
Linux:
```
$ ./flash-all.sh
```
Windows:
```
$ flash-all.bat
```
11. Use <b>fastboot</b> to lock your bootloader after flashing is completed and device rebooted
```
$ fastboot flashing lock
```
12. Use <b>fastboot</b> to reboot back to Android OS
```
$ fastboot reboot
```
13. Setup Android OS
14. Become A Developer
15. Enable USB Debugging

### Root Android OS with Magisk 
* This is needed to gain more control over the Andrid OS and gain the ability to become a superuser
* This is needed by Linux installation which needs <b>chroot</b>
* Loosely following steps of https://highonandroid.com/android-root/how-to-root-android-10-pixel-pixel-2-pixel-3-pixel-3a
1. Got to <b>Factory Images for Nexus and Pixel Devices</b> at https://developers.google.com/android/images
2. Download <b>8.1.0 (OPM1.171019.012, Jan 2018)</b> at https://dl.google.com/dl/android/aosp/sailfish-opm1.171019.012-factory-49ed1aec.zip 
3. You should have downloaded and unzipped the factory image file if you have reinstalled Android in the previous steps
4. Unzip the downloaded file 
5. Go to the unzipped image folder (exact path may differ)
```
$ cd ~/Downloads/sailfish-opm1.171019.012-factory-49ed1aec/sailfish-opm1.171019.012
```
6. Unzip the <b>image-sailfish-opm1.171019.012.zip</b>
7. Go to the unzipped image folder where <b>boot.img</b> exists (exact path may differ)
```
$ cd ~/Downloads/sailfish-opm1.171019.012-factory-49ed1aec/sailfish-opm1.171019.012/image-sailfish-opm1.171019.012
```
8. Push the <b>boot.img</b> to the phone's <b>Downloads</b> folder using <b>adb push</b>
```
$ adb push boot.img /sdcard/Download
```
9. Download <b>Magisk Manager v7.5.1</b> using <b>curl</b>
```
$ cd ~/Download
$ curl --output MagiskManager-v7.5.1.apk -L https://github.com/topjohnwu/Magisk/releases/download/manager-v7.5.1/MagiskManager-v7.5.1.apk
```
10. Install <b>Magisk Manager v7.5.1</b> using <b>adb install</b>
```
$ cd ~/Download
$ adb install MagiskManager-v7.5.1.apk
```
11. Run <b>Magisk Manager</b>
    1. Expect to see *Magisk is not install* with and <b>INSTALL</b> button next to it
    2. This means device is not rooted yet, when rooted this will show as installed

12. Install Magisk by clicking <b>INSTALL</b> and selecting <b>INSTALL</b>

13. Select <b>Select and Patch a File</b>

14. Find and patch <b>boot.img</b>
    1. Select the hamburger menu (three stacked lines) 
    2. Click on <b>Download</b>
    2. Select <b>boot.img</b>

15. If <b>boot.img</b> does no show up under <b>Downloads</b>
    1. Click on three dots and select <b>Show internal storage</b>
    2. Select the hamburger menu (three stacked lines) 
    3. Click on <b>Pixel</b>
    4. Select <b>Download</b> folder
    5. Select <b>boot.img</b>

16. Expect the device to freeze for 30 seconds
17. Expect a black screen with the message "*Output file is placed in <b>/storage/emulated/0/Download/magisk_patched.img</b>*"
18. Pull/download the <b>magisk_patched.img</b> to the computer's <b>Downloads</b> folder using <b>adb pull</b>
```
$ cd ~/Downloads
$ adb pull /storage/emulated/0/Download/magisk_patched.img
```
19. Use <b>adb</b> to restart in bootloader
```
$ adb reboot bootloader
```
20. Use <b>fastboot</b> to <b>*flash boot*</b> patched <b>magisk_patched.img</b> image
```
$ fastboot flash boot magisk_patched.img
```
21. Use <b>fastboot</b> to reboot back to Android OS
```
$ fastboot reboot
```
22. Run <b>Magisk Manager</b>
    1. Magisk Manager may fail to run, or freeze on start, may need few *Force stop*s before it runs - this is only happening on Android 8.1.0, did not happen on Android 7.1.2
    2. Expect to see *Magisk is up to date* with and <b>INSTALL</b> button next to it
    3. This means device is rooted yet

### Install Ubuntu OS on the Phone
* Rooted Android is required
* This will install a native Linux distribution on your Android device, this is not an emulation or a virtual operating system. Because of this, it will be able to use the whole resource potential of the device
* <b>chroot</b>, which points Linux installation to the underlying Android Kernel enabled Linux to share the same Kernel as the Android Kernel
1. Download <b>Linux Deploy</b> from Google <b>Play Store</b>
    1. If not found in search try this link https://play.google.com/store/apps/details?id=ru.meefik.linuxdeploy&hl=en_US
    2. If still not found in the Play Store use this link from <b>GitHub</b> https://github.com/meefik/linuxdeploy/releases/download/2.6.0/linuxdeploy-2.6.0-258.apk
2. Run <b>Linux Deploy</b>
3. Click on the <b>Properties/Setting</b> icon (three stacked lines that look like linear dials)
4. Set the properties, some properties already have the correct default values
    1. Distribution: <b>Ubuntu</b> (desktop Ubuntu distribution)
    1. Architecture: <b>arm64</b> (this needs to be changed to <b>armhf</b> on older devices)
    1. Distribution suite: <b>bionic</b> (18.04 LTS- Long Term Support version)
    1. Source path: <b>http://ports.ubuntu.com/</b>
    1. Installation path: <b>File</b> (install the whole Linux OS into a single image file, easiest and cleanest install and can be backed up by copying the image)
    1. Installation path: <b>$(EXTERNAL_STORAGE)/linux.img</b> (location of the OS image file)
    1. Image size: <b>24000</b> (24GB storage, default is 2GB and it is not nearly enough for installing ROS)
    1. User name: <b>android</b> (username for login, ssh and VNC/remote desktop)
    1. User password: <b>something</b> (some password of your liking)
    1. SSH - Enable: <b>checked</b>
    1. GUI - Enable: <b>checked</b>
    1. GUI - Graphics Subsystem: <b>X11</b> (graphics system; X11-like regular Ubuntu desktop, VNC-virtual desktop, FrameBuffer-?, VNC works fine, but ROS GUI-based apps like *imageviewer* won't work
    1. GUI - Desktop Environment: <b>MATE</b> (Ubuntu MATE style GUI, not as light as LXDE, but much usable)
    1. Click <b>back button</b> to get back to main screen
5. If exists, backup previous Ubuntu
```
$ adb pull /storage/emulated/0/linux.img
```
6. Install Ubuntu
    1. Click on <b>three dots</b>
    1. Click on <b>Install</b>
    1. This will overwrite you previous installation <b>linux.img</b>
    1. You can 
    1. Click on <b>OK</b>
    1. When completed expect to see ** message
7. On a fast wireless network installation takes 10 minutes
    1. 5 minutes to download
    1. 5 minutes to install

## References
* For rooting, loosely following https://highonandroid.com/android-root/how-to-root-android-10-pixel-pixel-2-pixel-3-pixel-3a
