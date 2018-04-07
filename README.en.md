

# ![Awesome Adb](./assets/title.png)

The [Android Debug Bridge](https://developer.android.com/studio/command-line/adb.html) (ADB) is a toolkit included in the Android SDK package, it is not only a powerful tool for Android developers and testers, but also a good toy for Android fans.

#test

This repository renews continually, Pull Requests and Issues are welcomed. If you found [this](https://github.com/mzlogin/awesome-adb) is useful, you can star it and conveniently back here to view when necessary.

**Note:** Some commands may depending on the version of Android system or ROM.

Other languages: [:cn: Chinese](./README.md)

# ![Table of Contents](./assets/toc.png)

<!-- vim-markdown-toc GFM -->

* [Basic Usage](#basic-usage)
    * [Command syntax](#command-syntax)
    * [Targeting equipment for command](#targeting-equipment-for-command)
    * [Start/Stop](#startstop)
    * [View adb version](#view-adb-version)
    * [Run adbd as root](#run-adbd-as-root)
    * [Designated adb server network port](#designated-adb-server-network-port)
* [Device connection management](#device-connection-management)
    * [Inquiries connected device / simulator](#inquiries-connected-device--simulator)
    * [USB connection](#usb-connection)
    * [Wireless connection (need to use the USB cable)](#wireless-connection-need-to-use-the-usb-cable)
    * [Wireless connection (without using the USB cable)](#wireless-connection-without-using-the-usb-cable)
* [Application Management](#application-management)
    * [Check the list of](#check-the-list-of)
        * [All applications](#all-applications)
        * [system applications](#system-applications)
        * [third-party usage](#third-party-usage)
        * [Application package name contains a string](#application-package-name-contains-a-string)
    * [Install APK](#install-apk)
    * [Uninstalling](#uninstalling)
    * [Clear app cache data](#clear-app-cache-data)
    * [View Reception Activity](#view-reception-activity)
    * [View Running Services](#view-running-services)
    * [Query package detail information](#query-package-detail-information)
    * [Query application installation path](#query-application-installation-path)
* [Interact with Applications](#interact-with-applications)
    * [Launch app / Start an Activity](#launch-app--start-an-activity)
    * [Start a Service](#start-a-service)
    * [Stop service](#stop-service)
    * [Send a broadcast](#send-a-broadcast)
    * [Force stop an application](#force-stop-an-application)
    * [Trim memory](#trim-memory)
* [File Management](#file-management)
    * [Copy files from a device to a computer](#copy-files-from-a-device-to-a-computer)
    * [Copy files from a computer to a device](#copy-files-from-a-computer-to-a-device)
* [Analog Keys / inputs](#analog-keys--inputs)
    * [Power button](#power-button)
    * [menu](#menu)
    * [HOME key](#home-key)
    * [return key](#return-key)
    * [volume control](#volume-control)
    * [Media Control](#media-control)
    * [On / Off screen](#on--off-screen)
    * [Slide to unlock](#slide-to-unlock)
    * [Enter text](#enter-text)
* [View Log](#view-log)
    * [Android log](#android-log)
    * [Filter the log by level](#filter-the-log-by-level)
        * [Filter by tag and log level](#filter-by-tag-and-log-level)
        * [Log format](#log-format)
        * [Clear log](#clear-log)
    * [Kernel log](#kernel-log)
* [View device information](#view-device-information)
    * [Model](#model)
    * [Battery Status](#battery-status)
    * [Screen Resolution](#screen-resolution)
    * [Screen density](#screen-density)
    * [Display Parameters](#display-parameters)
    * [android\_id](#android_id)
    * [IMEI](#imei)
    * [Android system version](#android-system-version)
    * [IP address](#ip-address)
    * [Mac Address](#mac-address)
    * [CPU Information](#cpu-information)
    * [Memory Information](#memory-information)
    * [More hardware and system properties](#more-hardware-and-system-properties)
* [Modify Settings](#modify-settings)
    * [Resolution](#resolution)
    * [Screen density](#screen-density-1)
    * [Overscan](#overscan)
    * [Turn off Android Debug](#turn-off-android-debug)
    * [Show/hide status bar or navigation bar](#showhide-status-bar-or-navigation-bar)
* [Utility functions](#utility-functions)
    * [Screenshots](#screenshots)
    * [Recording Screen](#recording-screen)
    * [Remount system partition as writable](#remount-system-partition-as-writable)
    * [Check connection over WiFi password](#check-connection-over-wifi-password)
    * [To set the system date and time](#to-set-the-system-date-and-time)
    * [restart cellphone](#restart-cellphone)
    * [Detect whether the device is root](#detect-whether-the-device-is-root)
    * [Monkey use stress testing](#monkey-use-stress-testing)
    * [On / off WiFi](#on--off-wifi)
* [Flashing-Phone related commands](#flashing-phone-related-commands)
    * [Restart to Recovery mode](#restart-to-recovery-mode)
    * [To restart from the Recovery Android](#to-restart-from-the-recovery-android)
    * [Restart to Fastboot mode](#restart-to-fastboot-mode)
    * [Through sideload system update](#through-sideload-system-update)
* [Security-related commands](#security-related-commands)
    * [Enable / Disable SELinux](#enable--disable-selinux)
    * [Enable / Disable dm_verity](#enable--disable-dm_verity)
* [More adb shell command](#more-adb-shell-command)
    * [See process](#see-process)
    * [View real-time resource consumption](#view-real-time-resource-consumption)
    * [query process uid](#query-process-uid)
    * [Other](#other)
* [common problem](#common-problem)
    * [Start adb server failure](#start-adb-server-failure)
    * [com.android.ddmlib.AdbCommandRejectedException](#comandroidddmlibadbcommandrejectedexception)
* [adb unofficial implementation](#adb-unofficial-implementation)
* [related commands](#related-commands)
* [Acknowledgements](#acknowledgements)
* [Reference Links](#reference-links)

<!-- vim-markdown-toc -->

## Basic Usage

### Command syntax

adb basic syntax of the command is as follows:

```sh
adb [-d|-e|-s <serialNumber>] <command>
```

If only one device / emulator connection, you can omit the `[-d | -e | -s <serialNumber>]` this part, the direct use `adb <command>`.

### Targeting equipment for command

If you have more than one device / emulator connection, you need to specify the target device for the command.

| Parameter           | Meaning                                                                           |
|---------------------|-----------------------------------------------------------------------------------|
| -d                  | Specifies currently the only Android device USB connector as the command target   |
| -e                  | Specify currently the only goal for the command to run the simulator              |
| `-s <SerialNumber>` | Specifies the device number corresponding serialNumber / simulator command target |

In the case of multiple devices / simulators are connected to the more common `-s <serialNumber>` parameters, serialNumber can be obtained through `adb devices` command. Such as:

```sh
$ adb devices

List of devices attached
cf264b8f	device
emulator-5554	device
```

Output in the `cf264b8f` and` emulator-5554` is serialNumber. For example, this time I want to specify `cf264b8f` this equipment to run the adb command to take a screen resolution:

```sh
adb -s cf264b8f shell wm size
```

Encountered multiple devices / simulators use the case of these parameters for the command to specify the target device, hereinafter to simplify the description will not be repeated.

### Start/Stop

Start adb server command:

```sh
adb start-server
```

(Generally no need to manually execute this command, when you run the command adb adb server if found does not start automatically from the transfer.)

Stop adb server command:

```sh
adb kill-server
```

### View adb version

command:

```sh
adb version
```

Sample output:

```sh
Android Debug Bridge version 1.0.36
Revision 8f855a3d9b35-android
```

### Run adbd as root

The operating principle is adb adb server daemon and the phone side PC side adbd establish a connection, then the PC side adb client via adb server forward command parsing after running adbd receive commands.

So if adbd ordinary rights to perform some require root privileges to execute the command can not be directly used `adb xxx` execution. Then you can then execute the command `adb shell` after` su`, but also allows adbd root privileges to perform this high privilege can execute arbitrary commands.

command:

```sh
adb root
```

Normal output:

```sh
restarting adbd as root
```

Now run `adb shell`, take a look at the command line prompt is not turned into a` `#?

After some phone root can not let adbd by `adb root` execute commands with root privileges, some models such as Samsung, will be prompted to` adbd can not run as root in production builds`, then you can install adbd Insecure, then `adb root` try.

Accordingly, if you want to restore adbd non-root privileges, you can use `adb unroot` command.

### Designated adb server network port

command:

```sh
adb -P <port> start-server
```

The default port is 5037.

## Device connection management

### Inquiries connected device / simulator

command:

```sh
adb devices
```

Example output:

```sh
List of devices attached
cf264b8f	device
emulator-5554	device
```

Output format is `[serialNumber] [state]`, serialNumber that is, we often say that the SN, state the following categories:

* `Offline` - indicates that the device is not connected to the success or unresponsive.

* `Device` - device is connected. Note that this state does not identify the Android system has been fully activated and operational in the device during startup device instance can be connected to the adb, but after boot the system before it becomes operational.

* `No device` - no device / emulator connection.

The output shows the current connected the two devices / simulators, `cf264b8f` and` emulator-5554` are they SN. As can be seen from the `emulator-5554` name it is an Android emulator.

Common alarm output:

1. No device / emulator connection is successful.

   ```sh
   List of devices attached
   ```

2. The device / emulator is not connected to adb or unresponsive.

   ```sh
   List of devices attached
   cf264b8f	offline
   ```

### USB connection

USB connection normal use adb by the need to ensure that:

1. Hardware status is normal.

   Including Android devices in the normal power state, USB cable and interface intact.

Developer Options 2. Android devices and USB debugging mode is on.

   You can go to the "Settings" - "Developer options" - "Android Debug" view.

   If you can not find the developer options in the settings, it needs to make it through an egg is displayed: In the "Settings" - "About phone" continuous click "version number" 7 times.

3. The device driver is normal.

   It seems to worry about the Linux and Mac OS X, the Windows likely to be encountered in the case of the need to install drivers, this can be confirmed right "Computer" - "Properties", the "Device Manager" in view on related equipment Is there a yellow exclamation point or question mark, if not explain the driving state has been good. Otherwise, you can download a mobile assistant class program to install the driver first.

4. Status after confirmation via USB cable connected computers and devices.

   ```sh
   adb devices
   ```

   If you can see

   ```sh
   xxxxxx device
   ```

   Description Connection successful.

### Wireless connection (need to use the USB cable)

In addition to the USB connection to the computer to use adb, can also be a wireless connection - although the connection process is also step using USB needs, but after a successful connection to your device can get rid of the limit of the USB cable within a certain range it !

Steps:

1. Connect Android device to run adb computer connected to the same local area network, such as connected to the same WiFi.

2. The device connected to the computer via a USB cable.

   Make sure the connection is successful (you can run `adb devices` see if you can list the device).

3. Allow the device listens on port 5555 TCP / IP connections:

   ```sh
   adb tcpip 5555
   ```

4. Disconnect the USB connection.

5. Find the IP address of the device.

   Generally the 'Settings' in - "About phone" - "state information" - "IP address" is found, you can also use the following in the [View device information - IP address][1] a Lane method adb command.

6. Connect the device via IP address.

   ```sh
   adb connect <device-ip-address>
   ```

   Here `<device-ip-address>` is the IP address of the device found in the previous step.

7. Confirm the connection status.

   ```sh
   adb devices
   ```

   If you can see

   ```sh
   <device-ip-address>:5555 device
   ```

   Description Connection successful.

If you can not connect, verify that Android devices and the computer is connected to the same WiFi, then execute `adb connect <device-ip-address>` that step again;

If that does not work, by `adb kill-server` restart the adb and then try it all over again.

**The wireless connection**

command:

```sh
adb disconnect <device-ip-address>
```

### Wireless connection (without using the USB cable)

**Note: You need root privileges.**

On a "wireless connection (need to use USB cable)" method is described in official documents, need the help of a USB cable to enable the wireless connection.

Since we want to achieve a wireless connection, it can all step down are wireless it? The answer is energy.

1. Install a terminal emulator on the Android device.

   Equipment already installed you can skip this step. Terminal emulator download address I use is: [Terminal Emulator for Android Downloads](https://jackpal.github.io/Android-Terminal-Emulator/)

2. To run the Android device and computer adb is connected to the same local area network, such as connected to the same WiFi.

3. Open a terminal emulator on your Android device, in which run the command sequence:

   ```sh
   su
   setprop service.adb.tcp.port 5555
   ```

4. Find the IP address of the Android device.

   Generally the 'Settings' in - "About phone" - "state information" - "IP address" is found, you can also use the following in the [View device information - IP address][1] a Lane method adb command.

5. Connect Android device on a computer via adb and IP addresses.

   ```sh
   adb connect <device-ip-address>
   ```

   Here `<device-ip-address>` is the IP address of the device found in the previous step.

   If you can see `connected to <device-ip-address>: 5555` such output indicates a successful connection.

* Notice: *
   Some device may not working unless you restart adbd service, so you need to run command on the device's terminal as below

   ```sh
   restart adbd
   ```

   if `restart` is not working, try following command:

   ```sh
   stop adbd
   start adbd
   ```

## Application Management

### Check the list of

Check the list of basic commands format

```sh
adb shell pm list packages [-f] [-d] [-e] [-s] [-3] [-i] [-u] [--user USER_ID] [FILTER]
```

That is the basis of `adb shell pm list packages` can add some parameters on the filter to view different lists, supports filtering parameters are as follows:

| Parameter  | display list                             |
|------------|------------------------------------------|
| No         | all applications                         |
| -f         | Display apk file application association |
| -d         | Show only applications disabled          |
| -e         | Show only enabled applications           |
| -s         | Display only System                      |
| -3         | Show only third-party application        |
| -i         | Display applications installer           |
| -u         | Contains uninstall applications          |
| `<FILTER>` | package name contains `<FILTER>` strings |

#### All applications

command:

```sh
adb shell pm list packages
```

Example output:

```sh
package:com.android.smoketest
package:com.example.android.livecubes
package:com.android.providers.telephony
package:com.google.android.googlequicksearchbox
package:com.android.providers.calendar
package:com.android.providers.media
package:com.android.protips
package:com.android.documentsui
package:com.android.gallery
package:com.android.externalstorage
...
// other packages here
...
```

#### system applications

command:

```sh
adb shell pm list packages -s
```

#### third-party usage

command:

```sh
adb shell pm list packages -3
```

#### Application package name contains a string

For example, to view a list of package names that contain the string `mazhuang` applications, order:

```sh
adb shell pm list packages mazhuang
```

Of course, you can also use grep to filter:

```sh
adb shell pm list packages | grep mazhuang
```

### Install APK

Format:

```sh
adb install [-lrtsdg] <path_to_apk>
```

parameter:

`Adb install` may be followed by some optional parameters to control the behavior of the installation APK, available parameters and their meanings are as follows:

| Parameter | Meaning                                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------------------|
| -l        | Will be applied to protect the installation directory / mnt / asec                                        |
| -r        | Allowed to cover the installation                                                                         |
| -t        | Allowed to install application specified in AndroidManifest.xml `android: testOnly =" true "` Application |
| -s        | Install apps to sdcard                                                                                    |
| -d        | Downgrade coverage allows installation                                                                    |
| -g        | Grant all runtime permissions                                                                             |

After you run the command to see if similar to the following output (status is `Success`) represents the installation was successful:

```sh
[100%] /data/local/tmp/1.apk
	pkg: /data/local/tmp/1.apk
Success
```

The above is the output of adb current latest version v1.0.36, it will push apk file to display the progress of the percentage of mobile phones.

Using older versions of adb output is this:

```sh
12040 KB/s (22205609 bytes in 1.801s)
        pkg: /data/local/tmp/SogouInput_android_v8.3_sweb.apk
Success
```

If the status is `Failure` said installation failure, such as:

```sh
[100%] /data/local/tmp/map-20160831.apk
        pkg: /data/local/tmp/map-20160831.apk
Failure [INSTALL_FAILED_ALREADY_EXISTS]
```

Common Installation failed output code, the meaning and possible solutions are as follows:

| Output                                                              | Meaning                                                                                                                                       | solutions                                                                    |
|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| INSTALL\_FAILED\_ALREADY\_EXISTS                                    | application already exists                                                                                                                    | use `-r` parameters                                                          |
| INSTALL\_FAILED\_INVALID\_APK                                       | invalid APK file                                                                                                                              |                                                                              |
| INSTALL\_FAILED\_INVALID\_URI                                       | invalid filename APK                                                                                                                          | APK file names to ensure no Chinese                                          |
| INSTALL\_FAILED\_INSUFFICIENT\_STORAGE                              | lack of space                                                                                                                                 | cleanup space                                                                |
| INSTALL\_FAILED\_DUPLICATE\_PACKAGE                                 | program of the same name already exists                                                                                                       |                                                                              |
| INSTALL\_FAILED\_NO\_SHARED\_USER                                   | shared user requested does not exist                                                                                                          |                                                                              |
| INSTALL\_FAILED\_UPDATE\_INCOMPATIBLE                               | already installed the app, but signature is not the same; or uninstalled, but data is not removed.                                            |                                                                              |
| INSTALL\_FAILED\_SHARED\_USER\_INCOMPATIBLE                         | shared user request exists but the signatures do not match                                                                                    |                                                                              |
| INSTALL\_FAILED\_MISSING\_SHARED\_LIBRARY                           | installation package used on the device unusable shared library                                                                               |                                                                              |
| INSTALL\_FAILED\_REPLACE\_COULDNT\_DELETE                           | can not be deleted when replacing                                                                                                             |                                                                              |
| INSTALL\_FAILED\_DEXOPT                                             | dex optimization validation failure or lack of space                                                                                          |                                                                              |
| INSTALL\_FAILED\_OLDER\_SDK                                         | equipment system version is lower than the application requirements                                                                           |                                                                              |
| INSTALL\_FAILED\_CONFLICTING\_PROVIDER                              | equipment already exists with the same name in application content provider                                                                   |                                                                              |
| INSTALL\_FAILED\_NEWER\_SDK                                         | equipment system version higher than the application requirements                                                                             |                                                                              |
| INSTALL\_FAILED\_TEST\_ONLY                                         | test-only applications, but when you install `-t` parameter is not specified                                                                  |                                                                              |
| INSTALL\_FAILED\_CPU\_ABI\_INCOMPATIBLE                             | contains incompatible device CPU Application Binary Interface for native code                                                                 |                                                                              |
| INSTALL\_FAILED\_MISSING\_FEATURE                                   | application uses device features that are unavailable                                                                                         |                                                                              |
| INSTALL\_FAILED\_CONTAINER\_ERROR                                   | sdcard access failure                                                                                                                         | confirm sdcard is available, or to install built-in storage                  |
| INSTALL\_FAILED\_INVALID\_INSTALL\_LOCATION                         | can not be installed to the specified location                                                                                                | switch mounting position, add or delete `-s` parameters                      |
| INSTALL\_FAILED\_MEDIA\_UNAVAILABLE                                 | installation location is unavailable                                                                                                          | generally sdcard, confirm sdcard is available or to install built-in storage |
| INSTALL\_FAILED\_VERIFICATION\_TIMEOUT                              | Installation Timeout verify                                                                                                                   |                                                                              |
| INSTALL\_FAILED\_VERIFICATION\_FAILURE                              | verify the installation package fails                                                                                                         |                                                                              |
| INSTALL\_FAILED\_PACKAGE\_CHANGED                                   | calling application program expects inconsistent                                                                                              |                                                                              |
| INSTALL\_FAILED\_UID\_CHANGED                                       | previously installed the app, and this assignment UID inconsistent                                                                            | remove residual files previously installed                                   |
| INSTALL\_FAILED\_VERSION\_DOWNGRADE                                 | already installed the application later                                                                                                       | use `-d` parameters                                                          |
| INSTALL\_FAILED\_PERMISSION\_MODEL\_DOWNGRADE                       | installed target SDK runtime support for application permissions of the same name, to install the runtime version does not support permission |                                                                              |
| INSTALL\_PARSE\_FAILED\_NOT\_APK                                    | specified path is not a file or not to `.apk` end                                                                                             |                                                                              |
| INSTALL\_PARSE\_FAILED\_BAD\_MANIFEST                               | unresolved AndroidManifest.xml file                                                                                                           |                                                                              |
| INSTALL\_PARSE\_FAILED\_UNEXPECTED\_EXCEPTION                       | parser encounters an exception                                                                                                                |                                                                              |
| INSTALL\_PARSE\_FAILED\_NO\_CERTIFICATES                            | installation package is not signed                                                                                                            |                                                                              |
| INSTALL\_PARSE\_FAILED\_INCONSISTENT\_CERTIFICATES                  | already installed the app, and signed with the APK files are inconsistent                                                                     | first uninstall the application on the device, then install                  |
| INSTALL\_PARSE\_FAILED\_CERTIFICATE\_ENCODING                       | encountered while parsing APK file `CertificateEncodingException`                                                                             |                                                                              |
| INSTALL\_PARSE\_FAILED\_BAD\_PACKAGE\_NAME                          | manifest file no or an invalid package name                                                                                                   |                                                                              |
| INSTALL\_PARSE\_FAILED\_BAD\_SHARED\_USER\_ID                       | manifest file specifies an invalid shared user ID                                                                                             |                                                                              |
| INSTALL\_PARSE\_FAILED\_MANIFEST\_MALFORMED                         | encountered while parsing file manifest error structural                                                                                      |                                                                              |
| INSTALL\_PARSE\_FAILED\_MANIFEST\_EMPTY                             | in the manifest file can not be found to find operable label (instrumentation or application)                                                 |                                                                              |
| INSTALL\_FAILED\_INTERNAL\_ERROR                                    | installation fails because of system problems                                                                                                 |                                                                              |
| INSTALL\_FAILED\_USER\_RESTRICTED                                   | Users are limited to installing applications                                                                                                  |                                                                              |
| INSTALL\_FAILED\_DUPLICATE\_PERMISSION                              | application attempts to define an existing permission name                                                                                    |                                                                              |
| INSTALL\_FAILED\_NO\_MATCHING\_ABIS                                 | applications include device application binary interface does not support the native code                                                     |                                                                              |
| INSTALL\_CANCELED\_BY\_USER                                         | applications installed on the device needs confirmation, but not operate the device or the point of cancellation                              | agree to install on the device                                               |
| INSTALL\_FAILED\_ACWF\_INCOMPATIBLE                                 | applications are not compatible with the device                                                                                               |                                                                              |
| Does not contain AndroidManifest.xml                                | invalid APK file                                                                                                                              |                                                                              |
| Is not a valid zip file                                             | invalid APK file                                                                                                                              |                                                                              |
| Offline                                                             | device is not connected successfully                                                                                                          | first device with adb successful connection                                  |
| Unauthorized                                                        | unauthorized device allows debugging                                                                                                          |                                                                              |
| Error: device not found                                             | not successfully connected equipment                                                                                                          | equipment and adb first successful connection                                |
| Protocol failure                                                    | device is disconnected                                                                                                                        | first device with adb successful connection                                  |
| Unknown option: -s                                                  | Android 2.2 does not support the following installation to sdcard                                                                             | do not use `-s` parameters                                                   |
| No space left on device                                             | lack of space                                                                                                                                 | cleanup space                                                                |
| Permission denied ... sdcard ...                                    | sdcard unavailable                                                                                                                            |                                                                              |
| signatures do not match the previously installed version; ignoring! | already installed this app, but signatures do not match                                                                                       | uninstall previous installed, then install this one                          |

Reference: [PackageManager.java](https://github.com/android/platform_frameworks_base/blob/master/core%2Fjava%2Fandroid%2Fcontent%2Fpm%2FPackageManager.java)

*`Adb install` internal principle Introduction*

`Adb install` actually three steps:

1. push apk files to / data / local / tmp.

2. Call pm install installation.

3. Delete the corresponding apk file / data / local / tmp under.

Therefore, when necessary, according to this step, manually step through the installation process.

### Uninstalling

command:

```sh
adb uninstall [-k] <packagename>
```

`<Packagename>` represents the application package name, `-k` optional parameter indicates uninstall the application but keep the data and cache directories.

Command Example:

```sh
adb uninstall com.qihoo360.mobilesafe
```

Uninstall represents 360 mobile guards.

### Clear app cache data

command:

```sh
adb shell pm clear <packagename>
```

`<Packagename>` represents the name of the application package, the effect of this command is equivalent to the application information in the settings screen, click the "Clear Cache" and "Clear data."

Command Example:

```sh
adb shell pm clear com.qihoo360.mobilesafe
```

360 mobile guards to clear the data and cache.

### View Reception Activity

command:

```sh
adb shell dumpsys activity activities | grep mFocusedActivity
```

Example output:

```sh
mFocusedActivity: ActivityRecord{8079d7e u0 com.cyanogenmod.trebuchet/com.android.launcher3.Launcher t42}
```

Where `com.cyanogenmod.trebuchet / com.android.launcher3.Launcher` is currently in the foreground Activity.

### View Running Services

command:

```sh
adb shell dumpsys activity services [<packagename>]
```

`<packagename>` parameter is optional, command with `<packagename>` will output services related with that packagename, and command without `<packagename>` will output all services.

Complete packagename is unnecessary. For example, `adb shell dumpsys activity services org.mazhuang` will output services related with `org.mazhuang.demo1`, `org.mazhuang.demo2` and `org.mazhuang123`, etc.

### Query package detail information

command:

```sh
adb shell dumpsys package <packagename>
```

There are many infos in output, include Activity Resolver Table, Registered ContentProviders, package name, userId, files/resources/codes path after install, version name and code, permissions info and their granted status, signing version, etc.

`<packagename>` is package name of an application.

Example output:

```sh
Activity Resolver Table:
  Non-Data Actions:
      android.intent.action.MAIN:
        5b4cba8 org.mazhuang.guanggoo/.SplashActivity filter 5ec9dcc
          Action: "android.intent.action.MAIN"
          Category: "android.intent.category.LAUNCHER"
          AutoVerify=false

Registered ContentProviders:
  org.mazhuang.guanggoo/com.tencent.bugly.beta.utils.BuglyFileProvider:
    Provider{7a3c394 org.mazhuang.guanggoo/com.tencent.bugly.beta.utils.BuglyFileProvider}

ContentProvider Authorities:
  [org.mazhuang.guanggoo.fileProvider]:
    Provider{7a3c394 org.mazhuang.guanggoo/com.tencent.bugly.beta.utils.BuglyFileProvider}
      applicationInfo=ApplicationInfo{7754242 org.mazhuang.guanggoo}

Key Set Manager:
  [org.mazhuang.guanggoo]
      Signing KeySets: 501

Packages:
  Package [org.mazhuang.guanggoo] (c1d7f):
    userId=10394
    pkg=Package{55f714c org.mazhuang.guanggoo}
    codePath=/data/app/org.mazhuang.guanggoo-2
    resourcePath=/data/app/org.mazhuang.guanggoo-2
    legacyNativeLibraryDir=/data/app/org.mazhuang.guanggoo-2/lib
    primaryCpuAbi=null
    secondaryCpuAbi=null
    versionCode=74 minSdk=15 targetSdk=25
    versionName=1.1.74
    splits=[base]
    apkSigningVersion=2
    applicationInfo=ApplicationInfo{7754242 org.mazhuang.guanggoo}
    flags=[ HAS_CODE ALLOW_CLEAR_USER_DATA ALLOW_BACKUP ]
    privateFlags=[ RESIZEABLE_ACTIVITIES ]
    dataDir=/data/user/0/org.mazhuang.guanggoo
    supportsScreens=[small, medium, large, xlarge, resizeable, anyDensity]
    timeStamp=2017-10-22 23:50:53
    firstInstallTime=2017-10-22 23:50:25
    lastUpdateTime=2017-10-22 23:50:55
    installerPackageName=com.miui.packageinstaller
    signatures=PackageSignatures{af09595 [53c7caa2]}
    installPermissionsFixed=true installStatus=1
    pkgFlags=[ HAS_CODE ALLOW_CLEAR_USER_DATA ALLOW_BACKUP ]
    requested permissions:
      android.permission.READ_PHONE_STATE
      android.permission.INTERNET
      android.permission.ACCESS_NETWORK_STATE
      android.permission.ACCESS_WIFI_STATE
      android.permission.READ_LOGS
      android.permission.WRITE_EXTERNAL_STORAGE
      android.permission.READ_EXTERNAL_STORAGE
    install permissions:
      android.permission.INTERNET: granted=true
      android.permission.ACCESS_NETWORK_STATE: granted=true
      android.permission.ACCESS_WIFI_STATE: granted=true
    User 0: ceDataInode=1155675 installed=true hidden=false suspended=false stopped=true notLaunched=false enabled=0
      gids=[3003]
      runtime permissions:
        android.permission.READ_EXTERNAL_STORAGE: granted=true
        android.permission.READ_PHONE_STATE: granted=true
        android.permission.WRITE_EXTERNAL_STORAGE: granted=true
    User 999: ceDataInode=0 installed=false hidden=false suspended=false stopped=true notLaunched=true enabled=0
      gids=[3003]
      runtime permissions:


Dexopt state:
  [org.mazhuang.guanggoo]
    Instruction Set: arm64
      path: /data/app/org.mazhuang.guanggoo-2/base.apk
      status: /data/app/org.mazhuang.guanggoo-2/oat/arm64/base.odex [compilation_filter=speed-profile, status=kOatUpToDa
      te]
```

### Query application installation path

command:

```
adb shell pm path <PACKAGE>
```

Output shows application installation path.



Example output:

```
adb shell pm path ecarx.weather

package:/data/app/ecarx.weather-1.apk
```

## Interact with Applications

The most used syntax for interacting with applications is :
```sh
am <command>
```
The common commands for `<command>` are as follow:

| Command                           | Use                                                  |
|-----------------------------------|------------------------------------------------------|
| `start [options] <INTENT>`        | Start an Activity specified by `<INTENT>`            |
| `startservice [options] <INTENT>` | Start the Service specified by `<INTENT>`            |
| `broadcast [options] <INTENT>`    | Send a broadcast `<INTENT>`                         |
| `force-stop <packagename>`        | Force stop everything associated with `<packagename>`|

The `<INTENT>` is a flexible parameter which is corresponding to the Intent writing in the application.

The options for `<INTENT>` are as follows:

| Parameter        | Meaning                                                                                                                               |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| `-a <ACTION>`    | Specify the intent action, such as `android.intent.action.VIEW`. You can declare this only once.                                                                                |
| `-c <CATEGORY>`  | Specify an intent category, such as `android.intent.category.APP_CONTACTS`                                                                    |
| `-n <COMPONENT>` | Specify the component name with package name prefix to create an explicit intent, such as `com.example.app/.ExampleActivity` |

There are some options addting data for `<INTENT>`, similar to `extra` for Bundle:

| Parameter                                                        | Meaning                                |
|------------------------------------------------------------------|----------------------------------------|
| `--esn <EXTRA_KEY>`                                              | null value (only key name)             |
| `-e|--es <EXTRA_KEY> <EXTRA_STRING_VALUE>`                       | string value                           |
| `--ez <EXTRA_KEY> <EXTRA_BOOLEAN_VALUE>`                         | boolean value                          |
| `--ei <EXTRA_KEY> <EXTRA_INT_VALUE>`                             | integer value                          |
| `--el <EXTRA_KEY> <EXTRA_LONG_VALUE>`                            | long value                             |
| `--ef <EXTRA_KEY> <EXTRA_FLOAT_VALUE>`                           | float value                            |
| `--eu <EXTRA_KEY> <EXTRA_URI_VALUE>`                             | URI                                    |
| `--ecn <EXTRA_KEY> <EXTRA_COMPONENT_NAME_VALUE>`                 | component name                         |
| `--eia <EXTRA_KEY> <EXTRA_INT_VALUE> [, <EXTRA_INT_VALUE ...]`   | integer array                          |
| `--ela <EXTRA_KEY> <EXTRA_LONG_VALUE> [, <EXTRA_LONG_VALUE ...]` | long array                             |

### Launch app / Start an Activity

The syntax is:

```sh
adb shell am start [options] <INTENT>
```

For example:

```sh
adb shell am start -n com.tencent.mm/.ui.LauncherUI
```

The command above means starting the launch activity of WeChat.

```sh
adb shell am start -n org.mazhuang.boottimemeasure/.MainActivity --es "toast" "hello, world"
```

The command above means starting MainActivity of the application with the package name `org.mazhuang.boottimemeasure` with an extra string information (key is 'toast' and value is 'hello, world').

### Start a Service

The syntax is:

```sh
adb shell am startservice [options] <INTENT>
```

For example:

```sh
adb shell am startservice -n com.tencent.mm/.plugin.accountsync.model.AccountAuthenticatorService
```

The command above means starting a service from WeChat.

### Stop service

The syntax is:

```sh
adb shell am stopservice [options] <INTENT>
```

### Send a broadcast

The syntax is:

```sh
adb shell am broadcast [options] <INTENT>
```

Broadcast intent can be sent to all components or a specified component.

For example, the command of issuing a broadcast intent with `BOOT_COMPLETED` to all of the components is as following:

```sh
adb shell am broadcast -a android.intent.action.BOOT_COMPLETED
```

As another example of issuing a broadcast intent with `BOOT_COMPLETED` only to `org.mazhuang.boottimemeasure / .BootCompletedReceiver` is as following:

```sh
adb shell am broadcast -a android.intent.action.BOOT_COMPLETED -n org.mazhuang.boottimemeasure/.BootCompletedReceiver
```

The command of issuing a broadcast intent is very useful in the test, especially when a broatcast intent is hard to generate normally, it would be of great use to send the broadcast intent by the command.

Both system predefined and custom broadcast intent are able to be sent. The following is part of the system predefined broadcast intents and the triggers:

| Action                                          | Trigger                                                               |
|-------------------------------------------------|-----------------------------------------------------------------------|
| android.net.conn.CONNECTIVITY_CHANGE            | network connectivity changes                                          |
| android.intent.action.SCREEN_ON                 | screen on                                                             |
| android.intent.action.SCREEN_OFF                | screen off                                                            |
| android.intent.action.BATTERY_LOW               | low battery, corresponding to the "Low battery warning" system dialog |
| android.intent.action.BATTERY_OKAY              | the battery is now okay after being low                               |
| android.intent.action.BOOT_COMPLETED            | device boot finished                                                  |
| android.intent.action.DEVICE_STORAGE_LOW        | low memory condition on the device                                    |
| android.intent.action.DEVICE_STORAGE_OK         | low memory condition on the device no longer exists                   |
| android.intent.action.PACKAGE_ADDED             | a new application has been installed                                  |
| android.net.wifi.STATE_CHANGE                   | WiFi connection status changed                                        |
| android.net.wifi.WIFI_STATE_CHANGED             | Wi-Fi has been enabled, disabled, enabling
