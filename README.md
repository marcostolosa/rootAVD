# rootAVD
### [newbit @ xda-developers](https://forum.xda-developers.com/m/newbit.1350876)
A Script to...
* root your Android Studio Virtual Device (AVD), with Magisk (Stable, Canary or Alpha)
* patch its fstab
* download and install the USB HOST Permissions Module for Magisk
* install custom build Kernel and its Modules
* download and install AOSP prebuilt Kernel and its Modules

...within seconds.

## Install Magisk
### Download rootAVD via
* [Click](https://github.com/newbit1/rootAVD/archive/refs/heads/master.zip)
* `git clone https://github.com/newbit1/rootAVD.git`

### Preconditions
* the AVD is running
* a working Internet connection for the Menu
* a command prompt / terminal is opened
* `adb shell` will connect to the running AVD

### How to Install ADB (Android SDK Platform-Tools)
* Open Android Studio -> SDK Manager -> Android SDK -> SDK Tools -> Check on **Android SDK Platform-Tools** -> Apply
<img src="https://user-images.githubusercontent.com/37043777/140064719-ea2dd704-1aea-4c38-9725-3edbdafe7924.png" width="200" height="200" />

## rootAVD Help Menu
```
rootAVD A Script to root AVD by NewBit XDA

Usage:	rootAVD [DIR/ramdisk.img] [OPTIONS] | [EXTRA_CMDS]
or:	rootAVD [ARGUMENTS]

Arguments:
	ListAllAVDs			Lists Command Examples for ALL installed AVDs

	EnvFixTask			Requires Additional Setup fix
					- construct Magisk Environment manual
					- only works with an already Magisk patched ramdisk.img
					- without [DIR/ramdisk.img] [OPTIONS] [PATCHFSTAB]
					- needed since Android 12 (S) rev.1
					- not needed anymore since Android 12 (S) API 31 and Magisk Alpha
					- Grant Shell Su Permissions will pop up a few times
					- the AVD will reboot automatically

	InstallApps			Just install all APKs placed in the Apps folder

Main operation mode:
	DIR				a path to an AVD system-image
					- must always be the 1st Argument after rootAVD
	
ADB Path | Ramdisk DIR:
	[M]ac/Darwin:			export PATH=~/Library/Android/sdk/platform-tools:$PATH
					~/Library/Android/sdk/system-images/android-$API/google_apis_playstore/x86_64/
	
	[L]inux:			export PATH=~/Android/Sdk/platform-tools:$PATH
					~/Android/Sdk/system-images/android-$API/google_apis_playstore/x86_64/
	
	[W]indows:			set PATH=%LOCALAPPDATA%\Android\Sdk\platform-tools;%PATH%
					%LOCALAPPDATA%\Android\Sdk\system-images\android-$API\google_apis_playstore\x86_64\
	
	$API:				25,29,30,S,etc.
	
Except for EnvFixTask, ramdisk.img must be untouched (stock).
	
Options:
	restore				restore all existing .backup files, but doesn't delete them
					- the AVD doesn't need to be running
					- no other Argument after will be processed
	
	InstallKernelModules		install custom build kernel and its modules into ramdisk.img
					- kernel (bzImage) and its modules (initramfs.img) are inside rootAVD
					- both files will be deleted after installation
	
	InstallPrebuiltKernelModules	download and install an AOSP prebuilt kernel and its modules into ramdisk.img
					- similar to InstallKernelModules, but the AVD needs to be online
	
Options are exclusive, only one at the time will be processed.
	
Extra Commands:
	DEBUG				Debugging Mode, prevents rootAVD to pull back any patched file
	
	PATCHFSTAB			fstab.ranchu will get patched to automount Block Devices like /dev/block/sda1
					- other entries can be added in the script as well
					- a custom build Kernel might be necessary

	GetUSBHPmodZ			The USB HOST Permissions Module Zip will be downloaded into /sdcard/Download
	
Extra Commands can be combined, there is no particular order.
	
Notes: rootAVD will
- always create .backup files of ramdisk.img and kernel-ranchu
- replace both when done patching
- show a Menu, to choose the Magisk Version (Stable || Canary || Alpha), if the AVD is online
- make the choosen Magisk Version to its local
- install all APKs placed in the Apps folder
```
### Linux & MacOS
```
Command Examples:
./rootAVD.sh
./rootAVD.sh ListAllAVDs
./rootAVD.sh EnvFixTask
./rootAVD.sh InstallApps

./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img restore
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img InstallKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG
```

<details>
<summary>Command Examples: for ALL installed AVDs</summary>

```
./rootAVD.sh
./rootAVD.sh ListAllAVDs
./rootAVD.sh EnvFixTask
./rootAVD.sh InstallApps

./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/android-automotive-playstore/x86/ramdisk.img
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/android-automotive-playstore/x86/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/android-automotive-playstore/x86/ramdisk.img restore
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/android-automotive-playstore/x86/ramdisk.img InstallKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/android-automotive-playstore/x86/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/android-automotive-playstore/x86/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG

./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/google_apis_playstore/x86_64/ramdisk.img
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/google_apis_playstore/x86_64/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/google_apis_playstore/x86_64/ramdisk.img restore
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/google_apis_playstore/x86_64/ramdisk.img InstallKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-29/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG

./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/x86_64/ramdisk.img
./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/x86_64/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/x86_64/ramdisk.img restore
./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/x86_64/ramdisk.img InstallKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG

./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img restore
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img InstallKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh ~/Library/Android/sdk/system-images/android-31/google_apis_playstore/x86_64/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG
```
</details>

### Windows
```
Command Examples:
rootAVD.bat
rootAVD.bat ListAllAVDs
rootAVD.bat EnvFixTask
rootAVD.bat InstallApps

rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img
rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img restore
rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img InstallKernelModules
rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules
rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG
```

<details>
<summary>Command Examples: for ALL installed AVDs</summary>

```
./rootAVD.bat
./rootAVD.bat ListAllAVDs
./rootAVD.bat EnvFixTask
./rootAVD.bat InstallApps

./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\android-automotive-playstore\x86\ramdisk.img
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\android-automotive-playstore\x86\ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\android-automotive-playstore\x86\ramdisk.img restore
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\android-automotive-playstore\x86\ramdisk.img InstallKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\android-automotive-playstore\x86\ramdisk.img InstallPrebuiltKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\android-automotive-playstore\x86\ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG

./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\google_apis_playstore\x86_64\ramdisk.img
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\google_apis_playstore\x86_64\ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\google_apis_playstore\x86_64\ramdisk.img restore
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\google_apis_playstore\x86_64\ramdisk.img InstallKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-29\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG

./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-30\google_apis_playstore\x86_64\ramdisk.img
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-30\google_apis_playstore\x86_64\ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-30\google_apis_playstore\x86_64\ramdisk.img restore
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-30\google_apis_playstore\x86_64\ramdisk.img InstallKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-30\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-30\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG

./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img restore
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img InstallKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules
./rootAVD.bat %LOCALAPPDATA%\Android\Sdk\system-images\android-31\google_apis_playstore\x86_64\ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG
```
</details>

### Notes
* Android 12 (S) API 31 is a 64 Bit Only System, needs Magisk Canary or Alpha
* With the new Menu, you can choose between the newest Magisk, Canary, Stable and Alpha, Version.
* Once choosen, the script will make that Version to your local one.
* Prebuilt Kernel and Modules will be pulled from [AOSP](https://android.googlesource.com/kernel/prebuilts)
* Starting Magisk from Terminal via `adb shell monkey -p com.topjohnwu.magisk -c android.intent.category.LAUNCHER 1`
* API 28 (Pie) is **not supported** at all -> [because](https://source.android.com/devices/bootloader/partitions/system-as-root#sar-partitioning)

### 2 Ways to boot the AVD into Safe Mode
* 1st Way - If the AVD still boots normal:
	* Tap and Hold the **Power Button** until the 3 Options appear
	* Tap and Hold the **Power Off Button** until **Reboot to safe mode** appears
* 2nd Way - If the AVD stuck while booting (**black** screen):
	* Tap and Hold the **Volume Down Button**
	* The Time Window is between the **Launching Emulator Bar** is approx **half way** until the **Google Boot Screen** appears
* Confirmation
	* On the Bottom Left Corner reads: **Safe mode**
	
### Automotive Notes
* After patching the ramdisk.img and cycle power, switch to user 0 via `adb shell am switch-user 0`
	* open the Magisk App and the **Requires Additional Setup** pops up -> reboot AVD
	* switch again to user 0
		* open the Magisk App -> Settings -> Multiuser Mode -> **User-Independent** -> reboot AVD
* Every time you want to Grant Su Permissions, switch to user 0 and then back to 10 `adb shell am switch-user 10`
* Alternative, you can install the Module [magisk-single-user](https://github.com/seebz/magisk-single-user)
	* and remove all user higher than 0 i.e. `adb shell pm remove-user 13` or `adb shell pm remove-user 10`

### Links
* [XDA [GUIDE] Build / Mod AVD Kernel Android 10 / 11 rootAVD [Magisk] [USB passthrough Linux] [Google Play Store API]](https://forum.xda-developers.com/t/guide-build-mod-avd-kernel-android10-x86_64-29-root-magisk-usb-passthrough-linux.4212719)
* [Inject Android Hardware USB HOST Permissions](https://github.com/newbit1/usbhostpermissons)
* [XDA [SCRIPT] rootAVD - root your Android Studio Virtual Device emulator with Magisk [Android 12][Linux][Darwin/MacOS][WIN][Google Play Store APIs]](https://forum.xda-developers.com/t/script-rootavd-root-your-android-studio-virtual-device-emulator-with-magisk-android-11-linux-darwin-macos-win-google-play-store-apis.4218123)
* [rootCROS - A Script to root your Google Chrome OS installed on a non Chromebook Device](https://github.com/newbit1/rootCROS)
* [Video - Android Studio Emulator (AVD) Rooting with Magisk using rootAVD](https://www.youtube.com/watch?v=JR4gDRYzY2c)

### XDA [GUIDE] How to [Build|Mod|Update] a custom AVD Kernel and its Modules
* [[GUIDE][Build|Mod|Update][kernel-ranchu][goldfish][5.4][5.10][GKI][ramdisk.img][modules][rootAVD][Android 11(R) 12(S)][AVD][Google Play Store API]](https://forum.xda-developers.com/t/guide-build-mod-update-kernel-ranchu-goldfish-5-4-5-10-gki-ramdisk-img-modules-rootavd-android-11-r-12-s-avd-google-play-store-api.4220697)

### How to root AVDs without Play Store (Google APIs) out of the box
### Windows
* open a terminal -> win + r `cmd`
	* add emulator to your PATH
	* find your AVD
	* launch your AVD with the `-writable-system` argument
	```
	set PATH=%LOCALAPPDATA%\Android\Sdk\emulator;%PATH%
	emulator -list-avds
		Pixel_4_API_28
	emulator -avd Pixel_4_API_28 -writable-system
	```
* open a 2nd terminal -> win + r `cmd`
	* enter the following commands one by one
	```
	set PATH=%LOCALAPPDATA%\Android\Sdk\platform-tools;%PATH%
	adb root
	adb shell avbctl disable-verification
	adb disable-verity
	adb reboot
	adb root
	adb remount
	adb shell
	generic_x86_64:/ #
	```

### Compatibility Chart
<table>
	<tr>
		<th rowspan="2"align="center">Android</th>
		<th rowspan="2"align="center">PlayStore</th>
		<th rowspan="2"align="center">API Level</th>
		<th rowspan="2"align="center">Rev.</th>
		<th rowspan="2"align="center">CPU/ABI</th>
		<th rowspan="2"align="center">Arch</th>
		<th rowspan="2"align="center">Build</th>
		<th colspan="3"align="center">Magisk v23.0</th>
	</tr>
	<tr>
		<th>Stable</th>
		<th>Canary</th>
		<th>Alpha</th>
	</tr>
	<tr>
		<td rowspan="4"align="center">12 (S)</td>
		<td rowspan="20"align="center"><img src="https://user-images.githubusercontent.com/37043777/140272882-10a9b396-550c-40c7-b809-2ca05527f7a5.png" width="15"/></td>
		<td rowspan="2"align="center">32 (Sv2)</td>
		<td rowspan="2"align="center">r01</td>
		<td rowspan="2"align="center">x86_64</td>
		<td rowspan="5"align="center">64-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-Sv2_r01-windows.zip">Windows</a></td>
		<td rowspan="5"align="center">:x:</td>
		<td rowspan="20"align="center">:heavy_check_mark:</td>
		<td rowspan="20"align="center">:heavy_check_mark:</td>
	</tr>
	<tr>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-Sv2_r01-darwin.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td rowspan="2"align="center">31</td>
		<td rowspan="2"align="center">r08</td>
		<td align="center">ARM 64 v8a</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/arm64-v8a-31_r08-darwin.zip">(M1) Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td align="center">x86_64</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-31_r08-darwin.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td rowspan="5"align="center">11 (R)</td>
		<td rowspan="5"align="center">30</td>
		<td rowspan="3"align="center">r10</td>
		<td align="center">ARM 64 v8a</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/arm64-v8a-30_r10-darwin.zip">(M1) Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td rowspan="2"align="center">x86_64</td>
		<td rowspan="2"align="center">32-Bit<br/>64-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-darwin.zip">Darwin<br/>MacOS</a></td>
		<td rowspan="15"align="center">:heavy_check_mark:</td>
	</tr>
	<tr>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-windows.zip">Windows</a></td>
	</tr>
	<tr>
		<td rowspan="2"align="center">r09</td>
		<td rowspan="2"align="center">x86</td>
		<td rowspan="2"align="center">32-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-30_r09-darwin.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-30_r09-windows.zip">Windows</a></td>
	</tr>
	<tr>
		<td rowspan="4"align="center">10 (Q)</td>
		<td rowspan="4"align="center">29</td>
		<td rowspan="4"align="center">r08</td>
		<td rowspan="2"align="center">x86_64</td>
		<td rowspan="2"align="center">32-Bit<br/>64-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-29_r08-windows.zip">Windows</a></td>
	</tr>
	<tr>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-29_r08-darwin.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td rowspan="4"align="center">x86</td>
		<td rowspan="4"align="center">32-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-29_r08-windows.zip">Windows</a></td>
	</tr>
	<tr>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-29_r08-darwin.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td align="center">8 (Oreo)</td>
		<td align="center">26</td>
		<td align="center">r07</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-26_r07.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td align="center">7 (Nougat)</td>
		<td align="center">24</td>
		<td align="center">r19</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-24_r19.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td align="center">TV 11 (R)</td>
		<td align="center">30</td>
		<td rowspan="2"align="center">r03</td>
		<td rowspan="3"align="center">x86</td>
		<td rowspan="3"align="center">32-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/android-tv/x86-30_r03.zip">Windows</a></td>
	</tr>
	<tr>
		<td align="center">TV 10 (Q)</td>
		<td align="center">29</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/android-tv/x86-29_r03.zip">Windows</a></td>
	</tr>
	<tr>
		<td align="center">Wear 8 (Oreo)</td>
		<td align="center">26</td>
		<td align="center">r04</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/android-wear/x86-26_r04.zip">Darwin<br/>MacOS</a></td>
	</tr>
	<tr>
		<td align="center">Automotive 11 (R)</td>
		<td align="center">30</td>
		<td rowspan="2"align="center">r01</td>
		<td align="center">x86_64</td>
		<td align="center">32-Bit<br/>64-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/android-automotive/x86_64-30_r01.zip">Windows</a></td>
	</tr>
	<tr>
		<td align="center">Automotive 10 (Q)</td>
		<td align="center">29</td>
		<td align="center">x86</td>
		<td align="center">32-Bit</td>
		<td align="center"><a href="https://dl.google.com/android/repository/sys-img/android-automotive/x86-29_r01.zip">Windows</a></td>
	</tr>
</table>

<details>
<summary>Archive</summary>
### Magisk v23.0 Alpha Successfully tested with Stock Kernel on
* [[Oct. 2021] - Android 12 (S) API 32 Google Apis Play Store x86_64 Sv2 r01 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-Sv2_r01-windows.zip)
* [[Oct. 2021] - Android 12 (S) API 32 Google Apis Play Store x86_64 Sv2 r01 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-Sv2_r01-darwin.zip)
* [[Oct. 2021] - Android 12 (S) API 31 Google Apis Play Store ARM 64 v8a r08 (M1) Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/arm64-v8a-31_r08-darwin.zip)
* [[Oct. 2021] - Android 11 (R) API 30 Google Apis Play Store ARM 64 v8a r10 (M1) Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/arm64-v8a-30_r10-darwin.zip)
* [[Oct. 2021] - Android 12 (S) API 31 Google Apis Play Store x86_64 r08 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-31_r08-darwin.zip)
* [[Oct. 2021] - Android 11 (R) API 30 Google Apis Play Store x86 r09 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-30_r09-darwin.zip)
* [[Oct. 2021] - Android 11 (R) API 30 Google Apis Play Store x86_64 r10 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-darwin.zip)

### Magisk v22.1+ Successfully tested with Stock Kernel on
* [[Oct. 2021] - Android  8 (Oreo) API 26 Google Apis Play Store x86 r07 Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-26_r07.zip)
* [[Oct. 2021] - Android  7 (Nougat) API 24 Google Apis Play Store x86 r19 Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-24_r19.zip)
* [[Oct. 2021] - Android  7 (Nougat) API 24 Google Apis x86_64 r27 Production Build](https://dl.google.com/android/repository/sys-img/google_apis/x86_64-24_r27.zip)
* [[Oct. 2021] - Android 11 (R) API 30 Google Apis Play Store x86 r09 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-30_r09-windows.zip)
* [[Oct. 2021] - Android 10 (Q) API 29 Google Apis Play Store x86 r08 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-29_r08-windows.zip)
* [[Oct. 2021] - Android 11 (R) API 30 Google Apis Play Store x86 r09 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-30_r09-darwin.zip)
* [[Oct. 2021] - Android 10 (Q) API 29 Google Apis Play Store x86 r08 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-29_r08-darwin.zip)
* [[June 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r05 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r05-darwin.zip)
* [[Apr. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r04 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r04-darwin.zip)
* [[May. 2021] - Android Wear 8 (Oreo) API 26 Google Apis Play Store x86 r04 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/android-wear/x86-26_r04.zip)
* [[May. 2021] - Android TV 11 (R) API 30 Google Apis Play Store x86 r03 Windows Production Build](https://dl.google.com/android/repository/sys-img/android-tv/x86-30_r03.zip)
* [[May. 2021] - Android TV 10 (Q) API 29 Google Apis Play Store x86 r03 Windows Production Build](https://dl.google.com/android/repository/sys-img/android-tv/x86-29_r03.zip)
* [[May. 2021] - Android 10 (Q) API 29 Google Apis Play Store x86 r01 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/android-automotive/x86-29_r01.zip)
* [[Apr. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r03 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r03-windows.zip)
* [[Apr. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r03 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r03-darwin.zip)
* [[Mar. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r02 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r02-darwin.zip)
* [[Mar. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r01 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r01-darwin.zip)
* [[Mar. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r02 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r02-windows.zip)
* [[Mar. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r01 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-S_r01-windows.zip)
* [[Mar. 2021] - Android 12 (S) API 30 Google Apis Play Store x86_64 r01 Darwin/MacOS User Debug Build](https://dl.google.com/android/repository/sys-img/google_apis/x86_64-S_r01.zip)
* [[Mar. 2021] - Android 11 (R) API 30 Google Apis Play Store x86_64 r10 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-darwin.zip)
* [[Mar. 2021] - Android 11 (R) API 30 Google Apis Play Store x86_64 r10 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-windows.zip)
* [[Mar. 2021] - Android 10 (Q) API 29 Google Apis Play Store x86_64 r08 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-29_r08-darwin.zip)
* [[Mar. 2021] - Android 10 (Q) API 29 Google Apis Play Store x86_64 r08 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-29_r08-windows.zip)
	
</details>

### Change Logs
#### [February 2022]
* [General] - Updated to Magisk Stable Version 24.1

<details>
<summary>Archive</summary>

### Change Logs
#### [October 2021]
* [rootAVD.sh] - Added get Up-To-Date Script Routine if Script is broken
* [rootAVD.sh] - Updated LZ4 decompression Routine
* [rootAVD.sh] - Updated InstallPrebuiltKernelModules Routine to support ARM64 Kernels
* [rootAVD.sh] - Updated Busybox Extraction Routine
* [General] - Added Multiarch Busybox Binarys and 64-Bit Only Support
* [General] - Added Alpha Channel to the Menu
* [rootAVD.bat] - Added Shut Down Feature
* [rootAVD.sh] - Added Shut Down Feature
* [General] - Added Android 12 (S) API 31 Status
* [General] - Added Link to Android AppSecs Video about rootAVD
#### [July 2021]
* [rootAVD.bat] - Changed TestADB
* [General] - Added rootCROS Project to Links
#### [June 2021]
* [General] - Android 12 (S) r05
#### [May 2021]
* [General] - Updated to Magisk App v23.0
* [rootAVD.sh] - Added "AddRCscripts" Argument that **install all custom *.rc scripts, placed in the rootAVD folder, into ramdisk.img/overlay.d/sbin**
* [rootAVD.sh] - Added BusyBox Binary after the rootAVD script
* [rootAVD.bat] - Added ListAllAVDs and InstallApps as Arguments
* [rootAVD.sh] - Added "ListAllAVDs" Argument that **Lists Command Examples for ALL installed AVDs**
* [rootAVD.sh] - Added "InstallApps" Argument to **Just install all APKs placed in the Apps folder**			
* [rootAVD.bat] - Added comprehensive Help Menu
#### [Apr. 2021]
* [General] - Added comprehensive Help Menu
* [rootAVD.sh] - Changed "DEBUG" "PATCHFSTAB" "GetUSBHPmodZ" to Arguments
* [General] - Fixed some typos and functions
* [rootAVD.sh] - Add a Menu to choose the prebuilt Kernel and Modules Version to install
* [General] - Added "InstallPrebuiltKernelModules" download/update/install prebuilt kernel and modules
* [General] - Added 2 Ways to boot the AVD into Safe Mode
* [rootAVD.sh] - Added Android S rev 3 support
* [General] - Added "InstallKernelModules" update/install custom build kernel and modules
* [rootAVD.sh] - Added update_lib_modules function
* [General] - Added "restore" to put back your backup files
* [General] - Updated local Magisk App v22.1
* [rootAVD.sh] - Added Option to Download the USB HOST Permissions Module
#### [Mar. 2021]
* [General] - Add a Download Manager Function for bad TLS record using wget
* [rootAVD.bat] - Adjustments to run with the updated rootAVD.sh
* [General] - Add a Menu to choose the Magisk Version to install
* [rootAVD.sh] - Added EnvFixTask Argument to fix Requires Additional Setup in Android S
* [General] - Changed to BusyBox (D)ASH Standalone
* [General] - Re-Structured Script
* [rootAVD.sh] - Added "Additional Setup Required" manually for Android S
* [rootAVD.sh] - Updated shakalaca's Ramdisk Repack Routine
* [rootAVD.sh] - Added Compression Detection for LZ4 and GZ
* [General] - Fixed some bugs and typos
* [General] - Updated to Magisk App v22.0
### Magisk v21.4 Successfully tested with Stock Kernel on
* [[Jan. 2021] - Android 11 (R) API 30 Google Apis Play Store x86_64 r10 Darwin/MacOS Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-darwin.zip)
* [[Jan. 2021] - Android 11 (R) API 30 Google Apis Play Store x86_64 r10 Windows Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-windows.zip)
* [[Jan. 2021] - Android 11 (R) API 30 Google Apis Play Store x86_64 r10 Linux Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-30_r10-linux.zip)
* [[Jan. 2021] - Android 11 (R) API 30 Google Apis Play Store x86 r09 Linux Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-30_r09-linux.zip)
* [[Dec. 2019] - Android 10 (Q) API 29 Google Apis Play Store x86_64 r09 Linux Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86_64-29_r08-linux.zip)
* [[Dec. 2019] - Android 10 (Q) API 29 Google Apis x86_64 r11 User Debug Build](https://dl.google.com/android/repository/sys-img/google_apis/x86_64-29_r11.zip)
* [[Jan. 2021] - Android  7 (Nougat) API 24 Google Apis Play Store x86 r19 Production Build](https://dl.google.com/android/repository/sys-img/google_apis_playstore/x86-24_r19.zip)

</details>

### Credits
* [topjohnwu @ xda-developers](https://forum.xda-developers.com/m/topjohnwu.4470081)
* [topjohnwu Magisk File Host](https://github.com/topjohnwu/magisk-files)
* [topjohnwu Magisk](https://github.com/topjohnwu/Magisk)
* [shakalaca @ xda-developers](https://forum.xda-developers.com/m/shakalaca.1813976)
* [shakalaca MagiskOnEmulator](https://github.com/shakalaca/MagiskOnEmulator)
* [Akianonymus _json_value](https://gist.github.com/cjus/1047794#gistcomment-3313785)
* [Tad Fisher Android Nixpkgs](https://github.com/tadfisher/android-nixpkgs)
* [Sébastien Corne magisk-single-user](https://github.com/seebz)
* [remote-android Native Bridge Support in ReDroid](https://github.com/remote-android/redroid-doc/tree/master/native_bridge)
* [Android AppSec - for his wonderful little video about this script](https://www.youtube.com/c/AndroidAppSec)
* [vvb2060 Magisk Alpha](https://github.com/vvb2060/magisk_files/)
 
