# Steps to build the Android 1.0 sources

In this codelab I will guide you through the steps to build the Android 1.0 sources.

Prerequisites: You should have setup your Ubuntu 8 build environment by following the steps [here](BuildingTheBuildEnv.md).

## Downloading the Android 1.0 archive files.

The Android 1.0 archive files are in subfolder [archive](archive).
We need to download them to the Ubuntu 8 VM.
Normally, you would just run `git clone https://github.com/TorZidan/android-1.0.git` in Ubuntu; however, this is futile: you will encounter SSL errors. Updating your git binary to the latest does not help, 
as the SSL libraries being used are not part of `git`.

My best suggestion is to download the files onto your host OS (using `git clone https://github.com/TorZidan/android-1.0.git` 
or by downloading https://github.com/TorZidan/android-1.0/archive/refs/heads/main.zip and unziping it, or by using the GitHub Desktop app), 
and then transfer them into a new folder `~/mydroid-1.0` on Ubuntu, using the VirtualBox file transfer utility (in the Ubuntu VM window, from the top-row menus, choose "Machine -> File Manager", enter your Ubuntu username & password, click on "Open Session" and then thransfer the files).

The instructions bellow assume that all archive failes are available on the Ubuntu VM, in folder `~/mydroid-1.0/archive`.

## Extracting the Android 1.0 archive files.

```
cd ~/mydroid-1.0/archive
chmod +x ./unzip.sh
./unzip.sh ../sources
```

This will extract all files into folder `~/mydroid-1.0/sources`.

## Building the "image" files for use on HTC Dream (the 1st Android phone):

```
cd ~/mydroid-1.0/sources
export JAVA_HOME=~/java/jdk1.5.0_22
export PATH=~/java/jdk1.5.0_22/bin:$PATH
export ANDROID_JAVA_HOME=$JAVA_HOME
source ./build/envsetup.sh
make TARGET_PRODUCT=generic TARGET_SIMULATOR=false TARGET_BUILD_TYPE=release TARGET_ARCH=arm TARGET_OS=linux HOST_ARCH=x86 HOST_OS=linux HOST_BUILD_TYPE=releas BUILD_ID=TC4
```

Go get a coffee while it does its thing.

Basically, we are running the `make` command without specifying any build target, with a bunch of env. variables set, which guide the build process what to do. 

Note: this long "make" command is same as: `lunch 1` followed by just `make`. Here, "lunch" is a bash command that was defined by running `source ./build/envsetup.sh` above; when run, it just sets a bunch of env. variables.

Note: the `make` build process executes the build instructions in the `Makefile` found in the current folder, which, itself, invokes the build instructions in the `Android.mk` files found in many of the subfolders.

Note: `make` uses Ubuntu's gcc and g++ compilers (version 4.2.4) and a gcc/g++ crosscompiler for the 'arm' platform that comes with Android, in subfolder `prebuilt/linux-x86/toolchain/arm-eabi-4.2.1/bin`.
Using any older or newer version of these compilers will result in build errors.

Upon success, it should exit with:
```
...
Generated: (out/target/product/generic/android-info.txt)
Target system fs image: out/target/product/generic/obj/PACKAGING/systemimage_unopt_intermediates/system.img
Install system fs image: out/target/product/generic/system.img
Target ram disk: out/target/product/generic/ramdisk.img
Target userdata fs image: out/target/product/generic/userdata.img
```

As we can see, it stored the build results in subfolder "out". Here are some notable files:

```
ls -l out/target/product/generic
total 49016
-rw-r--r--  1 android android        7 2025-01-31 19:15 android-info.txt
-rw-r--r--  1 android android       57 2025-01-31 19:20 clean_steps.mk
drwxr-xr-x  4 android android     4096 2025-01-31 18:48 data
drwxr-xr-x 12 android android     4096 2025-01-31 19:15 obj
-rw-r--r--  1 android android   136987 2025-01-31 19:15 ramdisk.img
drwxr-xr-x  8 android android     4096 2025-01-31 19:15 root
drwxr-xr-x  4 android android     4096 2025-01-31 18:58 symbols
drwxr-xr-x 12 android android     4096 2025-01-31 19:15 system
-rw-------  1 android android 47900160 2025-01-31 19:15 system.img
-rw-------  1 android android  2059200 2025-01-31 19:15 userdata.img

ls -l out/host/linux-x86/bin/
total 27368
-rwxr-xr-x 1 android android 3204109 2025-01-31 18:26 aapt
-rwxr-xr-x 1 android android   29250 2025-01-31 18:25 acp
-rwxr-xr-x 1 android android     802 2024-12-18 21:48 activitycreator
-rwxr-xr-x 1 android android  330658 2025-01-31 18:44 adb
...
-rwxr-xr-x 1 android android  133534 2025-02-01 13:34 fastboot
...
```

The ".img" files above contain full "hard drive" (actually flash-memory drive) partitions populated with all necessary files for running Android, including the Linux kernel, the Android "framework", the "default Android apps (Phone, Browser, Maps, Contacts, Gmail,etc) and more.
They can be "flashed" onto an "HTC Dream" phone using the `fastboot` command (it transmitts them to the phone over a USB cable), 
or by preparing an "update.zip" file, placing it on an SD card, inserting it in the phone, and "flashing" the file from the phone's "recovery" screen.
Note: this would work only on phones that have the "Engineering SPL" installed; this SPL (Second Program Loader) can be found on the "Android Dev Phone 1" (aka ADP1),
which is a developer-friendly version of the HTC Dream phone, or on a "rooted" HTC Dream phone.

Note: the Linux kernel is not part of any of the ".img" files above; it is in a separate partition, in file `boot.img`. See further down for more info.

## Building the Android SDK for Linux

```
cd ~/mydroid-1.0/sources

# I needed to make this fix to get a successful build:
mkdir --parents  development/emulator/prebuilt/android-arm/
cp prebuilt/android-arm/kernel/kernel-qemu development/emulator/prebuilt/android-arm/kernel-qemu

export JAVA_HOME=~/java/jdk1.5.0_22
export PATH=~/java/jdk1.5.0_22/bin:$PATH
export ANDROID_JAVA_HOME=$JAVA_HOME
source ./build/envsetup.sh

make sdk
```

Take a hike while it does its thing.

Upon success, it should print:

```
...
Package SDK: out/host/linux-x86/sdk/android-sdk_eng.android_linux-x86.zip
SDK: warning: including GNU target out/target/product/generic/system/lib/libdbus.so
```

As we can see, it stored the build results in subfolder "out" (as with other build targets). Here are some notable files:

```
ls -l out/host/linux-x86/sdk/
total 82204
drwxrwx--- 5 android android     4096 2025-01-31 22:19 android-sdk_eng.android_linux-x86
-rw-r--r-- 1 android android 83742582 2025-01-31 22:20 android-sdk_eng.android_linux-x86.zip
-rw-r--r-- 1 android android   336496 2025-01-31 22:19 sdk_deps.mk
```

Interesting finding: the Android Emulator is part of the SDK. To run it:

```
out/host/linux-x86/sdk/android-sdk_eng.android_linux-x86/tools/emulator
```

A new window will open, with a picture of a purple-colored phone in it. The phone needs a few seconds to fully boot. Use the mouse, as if you were using your finger on a touchscreen. Surprisingly, the Browser app still works with (some) modern web sites, once you discard the SSL warning messages popping up. The Emulator uses Qemu (see https://www.qemu.org/) to emulate the Arm-based Android Linux OS on Ubuntu x86 cpu. Impressive!

## Building the Linux kernel

Subfolder `~/mydroid-1.0/sources/kernel` contains the Linux open source files for Linux kernel version v2.6.25. These files are not Android-specific. Below, we will build them for the ARM processor family "msm" (used in the 1st Android phone HTC Dream).

Before building the kernel. you must create a file `mydroid-1.0/sources/kernel/.config` which will guide the build process.

You have many options:

* Use a default `.config` file:
    ```
    cd mydroid-1.0/sources/kernel/
    make ARCH=arm msm_defconfig
    ```
* Create your own file:
     ```
    cd mydroid-1.0/sources/kernel/
    make ARCH=arm menuconfig
    ```
     This will launch an "editor". Navigate throug menus with "tab", and "enter". Do your edits. At the end, choose "Exit"; when prompted, save your work.
* If buildng the kernel for use in the Android emulator, then extract the config file from a running emulator:
   ```
   cd mydroid-1.0/sources/kernel/
   # Delete any previous .config file:
   rm .config
   # Launch the emulator and wait for it to fully boot up:
   ../out/host/linux-x86/sdk/android-sdk_eng.android_linux-x86/tools/emulator &
   # Copy file config.gz from the running emulator's Android VM filesystem to Ubuntu:
   ../out/host/linux-x86/sdk/android-sdk_eng.android_linux-x86/tools/adb pull /proc/config.gz .
   # Now you can close the emultor window.
   gunzip config.gz
   mv config .config
   ```
* If building for the HTC Dream phone, you will have to pull the config.gz file from a running phone using `adb`, similarly to the steps above. Make sure your phone is running build TC4-RC29 or TC4-RC30 (android 1.0). Make sure "usb debugging" is enabled on the phone, so that it will accept "adb" connections. Connect the phone to your PC using a mini-USB-to-USB-A cable, and follow steps similar to above.

Once we have a `.config` file ready:
```
cd mydroid-1.0/sources/kernel/

export PATH=~/mydroid-1.0/sources/prebuilt/linux-x86/toolchain/arm-eabi-4.2.1/bin:$PATH

# Observe that the ".config" file is present:
ls -la .config

make clean
make ARCH=arm CROSS_COMPILE=arm-eabi-
```

Come back in 2 minutes.

Upon success, it should print:
```
...
Kernel: arch/arm/boot/zImage is ready
```

Here is an example of the produced kernel image file:
```
ls -l arch/arm/boot/
total 2788
drwxr-xr-x 2 android android    4096 2024-12-18 15:20 bootp
drwxr-xr-x 2 android android    4096 2025-02-02 10:38 compressed
-rwxr-xr-x 1 android android 1890880 2025-02-02 10:38 Image
-rw-r--r-- 1 android android    1326 2024-12-18 15:20 install.sh
-rw-r--r-- 1 android android    2775 2024-12-18 15:20 Makefile
-rwxr-xr-x 1 android android  938348 2025-02-02 10:38 zImage
```

If we built it using the `.config` file from the emulator, then we can launch the emulator with the new kernel file:
```
../out/host/linux-x86/sdk/android-sdk_eng.android_linux-x86/tools/emulator -kernel arch/arm/boot/zImage
```

