
# This folder contains the Android open source files that are part of Android 1.0 

## Copyright, licensing, redistribution :
All files in this folder (except `linux-2.6.25.zip`) were downloaded from AOSP (the Android Open Source Project) at https://android.googlesource.com/platform/.
For each file, I have included the original URL from where I downloaded it, so that you can go and get it yourself if you want (provided that these URLs are still valid in the future). Each archive file is in "tar.gz" format; each archive contains multiple files. Inside each archive file, you can find one or more files named "NOTICE" or  "COPYING" or "LICENSE" or some other file that declares that this work can be freely copied and redistributed; also, most text files contain a "header" that describes the same. If you have concerns about using, modifying or redistributing these files, please follow the links below to the origin of each file, and study them.

In addition, file `linux-2.6.25.zip` was downloaded from  https://github.com/torvalds/linux/archive/refs/tags/v2.6.25.zip , whose license can be found at https://github.com/torvalds/linux/blob/master/COPYING.

Disclaimer: I am NOT the creator of these files. I am not associated in any ways with the Android Open Source Project. I am providing the files here as-is, without modifying them.


## What is Android 1.0?
Android is an operating system for "smartphones", developed by Google.

On October 21, 2008, Google and the Open Handset Alliance announced the availability of the Android platform source code to everyone, for free, under the new Android Open Source Project,
see https://web.archive.org/web/20081022173050/http://source.android.com/posts/opensource
; the same post is also here: https://www.openhandsetalliance.com/press_102108.html.

Android 1.0 is the initial version of these files.
Back in 2008 and 2009, the only commercially-available phone that was running the Android 1.0 operating system was the "HTC Dream" phone (models DREA100 and DREA110) for TMobile wireless carrier in USA.
It was also available in 2009 for the Rogers Wireless carrier in the United Kingdom (model DREA210).

Note: before that, in 2007, Google and HTC developed the "HTC Sooner" (model EXCA300), a prototype phone that looked like a typical BlueBerry "slab" smartphone, with no wi-fi, no touch screen; it was running pre-1.0 versions of Android (e.g. build htc-2065.0.8.0.0 from 2007-05-15); these versions are not open source; this phone was never commercially sold. Google chose to scrap that project, in favor of the "HTC Dream" phone. Apple announced the iPhone in Jan 2007 and it went on sale in June of that yeat. Very likely the iPhone had a lot to do with Google's decision.

Interestingly, Android-related posts appeared on the webs in Nov 2007 (or even earlier?), way before the Oct 2008 open-source announcement, e.g. [here](https://web.archive.org/web/20071116110943/http://benno.id.au/blog/). 

I can't resist sharing [this](https://news.ycombinator.com/item?id=22286111) discussion, as it lays out the "clash of the titans" of the mobile world, the demise of old corporate empires and the rise of new ones. Note: as any un-moderated online discussion, not everything in there is true, and you should take these individual oppinions with a "grain of salt".

Here is a brief list of the few first official Android builds for the "HTC Dream" TMobile phone in USA:

| Build name | Android version | Build date | Notes |
| :---:      | :---:           | :---:         | :---: |
| TC4-RC19   | ???             | ???           | it is mentioned in [this](https://android.clients.google.com/updates/signed-kila-ota-114235-prereq.TC4-RC19.zip) file name (no-longer available).|
| TC4-RC28   | ???             | ???           | it is mentioned in [this](https://android.clients.google.com/updates/signed-kila-ota-115247-prereq.TC4-RC19+RC28.zip) file name (no-longer available). |
| TC4-RC29   | Android 1.0     | Oct. 24, 2008 | |
| TC4-RC30   | Android 1.0     | Oct. 31, 2008 | |
| PLAT-RC33  | Android 1.1 ("Petit Four")     | Jan. 16, 2009 | |
| CRB43      | Android 1.5 ("Cupcake")        | May. 13, 2009 | |
| DRC83      | Android 1.6_r1.1 ("Donut")     | Sep. 21, 2009 | |
| DMD64      | Android 1.6_r1.5 ("Donut")     | Dec. 3,  2009 | |

## Why did I store these files here?
As I describe further down, there is no easy way to discover these files, at https://android.googlesource.com/platform/.
Also, we don't know if these files will be available in the future , so I stored them here.

This is, basically, preservation of historical artifacts that profoundly changed our lives forever.

## What can you do with these files?

Once you download these files on a Linux PC, use the [unzip.sh](unzip.sh) shell script to recreate the android-1.0 source file tree, and then build the project (instructions are coming soon).

These files, along with a working HTC Dream phone, offer the perfect environment for learning C, C++, Linux, Java and the Android framework. Unlike bulky vintage computers from earlier eras, the HTC phone is a full-fledged vintage device that is easy to program, has tons of interesting software, and fits in your pocket. The Android emulator and simulator (these are two different things) are both here; they run on Linux, Windows and Mac, and offer an easy way of "kicking the tires", even if you don't have an Android phone.

## How do we know that the files below are for Android 1.0?
Upon successful build, there will be a subfolder "out", where we can find file `build.prop`:

```
cat  out/target/product/generic/system/build.prop 
  # begin build properties
  # autogenerated by buildinfo.sh
  ro.build.id=TC3
  ro.build.version.incremental=eng.android.20241228.130537
  ro.build.version.sdk=1
  ro.build.version.release=1.0
  ...
```

Upon further digging, I found out that the version "1.0" above comes from 
`PLATFORM_VERSION := 1.0` in file `build/core/version_defaults.mk`
which is part of the archive file `build.git-b6c1cf6de79035f58b512f4400db458c8401379a.tar.gz`

This also matches well with the `build.prop` file from an HTC Dream phone running Android-1.0:

```
adb shell "cat /system/build.prop"
  # begin build properties
  # autogenerated by buildinfo.sh
  ro.build.id=TC4-RC29
  ro.build.version.incremental=115247
  ro.build.version.sdk=1
  ro.build.version.release=1.0
  ro.build.date=Fri Oct 24 15:44:43 PDT 2008
  ...
```

Interestingly, that prod release build was made on Oct 24 2008, just 3 days after the AOSP announcement on Oct 21, 2008.

## Where were these files available back in 2008 ?
In 2008, you could get all these files via "repo sync",
as described at https://web.archive.org/web/20081022180011/http://source.android.com/download :

```
mkdir mydroid && cd mydroid
repo init -u git://android.git.kernel.org/platform/manifest.git
repo sync
```

Unfortunately, the android.git.kernel.org" git repository is no-longer available.

Fortunately, the same files are available at https://android.googlesource.com/platform .

If they were "tagged" as e.g. "android-1.0", we could use the most-recent "repo init && repo sync" commands to download them; 
unfortunately, there is no such tag (the oldest tag in these git repositories is "android-1.6_r1"). 

Fortunately, all these files were commited all at the same time,
on `Tue Oct 21 07:00:00 2008 -0700`, the same day when the Android Open Source Project was announced,
by `The Android Open Source Project <initial-contribution@android.com>`.

There are hundreds of Git repositories at https://android.googlesource.com/platform, all part of AOSP.
I had to sift through these hundreds of repositories and millions of commits to gather the files below.

## How can we tell which files comprise Android 1.0?
At https://web.archive.org/web/20081029052635/http://source.android.com/projects I found a high-level list of the git projects that were part of Android 1.0:
```
Project                    Description
bionic :                   C runtime: libc, libm, libdl, dynamic linker
bootloader/legacy :        Bootloader reference code
build :                    Build system
dalvik :                   Dalvik virtual machine
development :              High-level development and debugging tools
external                   External software that this project uses and depends on
frameworks/base :          Core Android app framework libraries
frameworks/policies/base : Framework configuration policies
hardware/libhardware :     Hardware abstraction library
hardware/ril :             Radio interface layer
kernel  (<<<most likely this is a typo, they mean "kernel/msm">>>):  Linux kernel
prebuilt:                  Binaries to support Linux and Mac OS builds
recovery :                 System recovery environment
system/bluetooth :         Bluetooth tools
system/core :              Minimal bootable environment
system/extras :            Low-level debugging/inspection tools
system/wlan/ti :           TI 1251 WLAN driver and tools
I added this one to the list:
vendor/htc/dream-open:     Files relevant only to the HTC Dream phone (and perhaps to the Android Developer Phone 1)
```

However, the info above is not sufficient to find the full list of files.
Then I found file https://android.googlesource.com/platform/manifest/+/refs/heads/android-1.6_r1/default.xml (part of Android 1.6).
This is the earliest such file. It instructs "repo init" which Git repository to download into which local folder.
I had to go through through each line in this file, look for it's corresponding Android-1.0 .tar.gz file at https://android.googlesource.com/platform , 
then manually download it (see below for more info); some lines in this file were introduced after Android-1.0 and therefore I skipped them. 


## Was it challenging to find these files?
It was a tedious process. Example:
Let's say we are in Git repository https://android.googlesource.com/platform/system/wlan/ti,
looking for a commit on `Tue Oct 21 07:00:00 2008 -0700` by `The Android Open Source Project <initial-contribution@android.com>`.
I had to navigate to the oldest tag "android-1.6_r1",
(e.g. https://android.googlesource.com/platform/system/wlan/ti/+/refs/tags/android-1.6_r1),
then click on the "log" link to view commits that occurred at and before this tag; in some git repositories, like this one,
there were just a few commits, so I could see the "Initial Contribution" commit right there on the page. 
However, in active and larger repositories I had to click "Next" at the bottom of the page hundreds of times until I got to that very first "Initial Contribution" commit.
I wrote a tiny javascript piece of code that I could run from the Chrome browser developer console, which would locate and click on the "Next" button on the page for me.

## Anatomy of a Git repository:
The android open source files are spread across multiple Git repositories. Once you choose which tag you want,
you can check it out on your Linux pc (this works as of Dec 2024):
"repo init --partial-clone -b android-1.6_r1  -u https://android.googlesource.com/platform/manifest && repo sync"
The "repo" python script reads the "Manifest" file (named "default.xml")
from e.g. https://android.googlesource.com/platform/manifest/+/3dbf7a37083842030d67082219af4b6a09f1a12b/default.xml ; It directs "repo" which Git repositories to fetch, into which subfolder.
Since there is no-longer a git tag named "android-1.0", I can't use "repo init" to download these files. Instead, I had to discover and manually download all files below,
which, when unzipped into the correct subfolder, will give us the full set of the Android 1.0 files.
One such repository is https://android.googlesource.com/platform/system/wlan/ti.git, which is same as https://android.googlesource.com/platform/system/wlan/ti
From that web page I can easily navigate to all branches and tags: 
Below "Tags", click on the "More ..." link to view all tags. 
Then find on the web page tag "android-1.6_r1" and click on it.
We get to page https://android.googlesource.com/platform/system/wlan/ti/+/refs/tags/android-1.6_r1 , from where we can download all files at that tag
by clicking on the "tgz" link.

## List of all files
Below is a list of all files that comprise Android 1.0.

Again: once you download these files on a Linux PC, use the [unzip.sh](unzip.sh) shell script to recreate the android-1.0 source file tree.

### Git project "platform/bionic": contains the C runtime: libc, libm, libdl, dynamic linker.

File bionic-a27d2baa0c1a2ec70f47ea9199b1dd6762c8a349.tar.gz

Downloaded from https://android.googlesource.com/platform/bionic/+/a27d2baa0c1a2ec70f47ea9199b1dd6762c8a349

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/bootable/recovery": System recovery environment

File recovery-23580ca27a0a8109312fdd36cc363ad1f4719889.tar.gz

Downloaded from https://android.googlesource.com/platform/bootable/recovery/+/23580ca27a0a8109312fdd36cc363ad1f4719889

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/bootable/bootloader/legacy": Bootloader reference code

File legacy-4205b865141ff2e255fe1d3bd16de18e217ef06a.tar.gz

Downloaded from https://android.googlesource.com/platform/bootable/bootloader/legacy/+/4205b865141ff2e255fe1d3bd16de18e217ef06a

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/build": Build system

File build.git-b6c1cf6de79035f58b512f4400db458c8401379a.tar.gz

Downloaded from https://android.googlesource.com/platform/build.git/+/b6c1cf6de79035f58b512f4400db458c8401379a

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/dalvik": Dalvik virtual machine (Why not call it Java?)

File dalvik.git-2ad60cfc28e14ee8f0bb038720836a4696c478ad.tar.gz

Downloaded from https://android.googlesource.com/platform/dalvik.git/+/2ad60cfc28e14ee8f0bb038720836a4696c478ad

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/development": High-level development and debugging tools

File development-5c11852110eeb03dc5a69111354b383f98d15336.tar.gz

Downloaded from https://android.googlesource.com/platform/development/+/5c11852110eeb03dc5a69111354b383f98d15336

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/aes":

File aes-045e5c3c0c0154d54e7abd95bf6505ddfff27dee.tar.gz

Downloaded from https://android.googlesource.com/platform/external/aes/+/045e5c3c0c0154d54e7abd95bf6505ddfff27dee

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/apache-http":

File apache-http-417f3b92ba4549b2f22340e3107d869d2b9c5bb8.tar.gz

Downloaded from https://android.googlesource.com/platform/external/apache-http/+/417f3b92ba4549b2f22340e3107d869d2b9c5bb8

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/bluez":

File bluez-611c26d196ef15425ae92dec9f3cdf92bbbe489a.tar.gz

Downloaded from https://android.googlesource.com/platform/external/bluez/+/611c26d196ef15425ae92dec9f3cdf92bbbe489a

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/clearsilver":

File clearsilver-5287bd68df69562fb14b988db841dd45b549e328.tar.gz

Downloaded from https://android.googlesource.com/platform/external/clearsilver/+/5287bd68df69562fb14b988db841dd45b549e328

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/dbus":

File dbus-7b0daf50cdb48a342490b35b83d80f80ee71915a.tar.gz

Downloaded from https://android.googlesource.com/platform/external/dbus/+/7b0daf50cdb48a342490b35b83d80f80ee71915a

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/dhcpcd":

File dhcpcd-e95877ecfa1170d77b1ec1f66752725cdda01b64.tar.gz

Downloaded from https://android.googlesource.com/platform/external/dhcpcd/+/e95877ecfa1170d77b1ec1f66752725cdda01b64

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/dropbear":

File dropbear-98b10356d53e48ffa482d72a36ec267ae5ea1dcc.tar.gz

Downloaded from https://android.googlesource.com/platform/external/dropbear/+/98b10356d53e48ffa482d72a36ec267ae5ea1dcc

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/elfcopy":

File elfcopy-130444ec10d2a40e2b3ede4863ab005aa1f4580c.tar.gz

Downloaded from https://android.googlesource.com/platform/external/elfcopy/+/130444ec10d2a40e2b3ede4863ab005aa1f4580c

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/elfutils":

File elfutils-593c365a822e505dae3aaa4d8d66eca333911624.tar.gz

Downloaded from https://android.googlesource.com/platform/external/elfutils/+/593c365a822e505dae3aaa4d8d66eca333911624

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/emma":

File emma-a0c5294bd396e480cbf850bde283a94042526698.tar.gz

Downloaded from https://android.googlesource.com/platform/external/emma/+/a0c5294bd396e480cbf850bde283a94042526698

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/esd":

File esd-53f215a8fd2333401e6ebc681581ad335726a0a7.tar.gz

Downloaded from https://android.googlesource.com/platform/external/esd/+/53f215a8fd2333401e6ebc681581ad335726a0a7

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/expat":

File expat-8a666ab336063fc53e446702fdf9ffe14af69e71.tar.gz

Downloaded from https://android.googlesource.com/platform/external/expat/+/8a666ab336063fc53e446702fdf9ffe14af69e71

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/fdlibm":

File fdlibm-8771baa10b2dc5bbedb08231d99c72cfd6abcb5b.tar.gz

Downloaded from https://android.googlesource.com/platform/external/fdlibm/+/8771baa10b2dc5bbedb08231d99c72cfd6abcb5b

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/freetype":

File freetype-a38fc482eeeb2c1929803c233835369dcf1b8781.tar.gz

Downloaded from https://android.googlesource.com/platform/external/freetype/+/a38fc482eeeb2c1929803c233835369dcf1b8781

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution



### Git project "platform/external/gdata":

File gdata-27eda2eccd3729366a5545a21238ee9b2960171c.tar.gz

Downloaded from https://android.googlesource.com/platform/external/gdata/+/27eda2eccd3729366a5545a21238ee9b2960171c

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/giflib":

File giflib-56f1b66a4b20a7f85865c852dd46df5e4635a9d6.tar.gz

Downloaded from https://android.googlesource.com/platform/external/giflib/+/56f1b66a4b20a7f85865c852dd46df5e4635a9d6

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/googleclient":

File googleclient-0dc808d29e2df4178f51efb62ecb32656f1533ad.tar.gz

Downloaded from https://android.googlesource.com/platform/external/googleclient/+/0dc808d29e2df4178f51efb62ecb32656f1533ad

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/icu4c":

File icu4c-43ebef775dab9dd52bc39eb98f306be1b3adbc8a.tar.gz

Downloaded from https://android.googlesource.com/platform/external/icu4c/+/43ebef775dab9dd52bc39eb98f306be1b3adbc8a

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/iptables":

File iptables-15630edb6b7f5ba40c572c43db13342243c23f10.tar.gz

Downloaded from https://android.googlesource.com/platform/external/iptables/+/15630edb6b7f5ba40c572c43db13342243c23f10

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/jdiff":

File jdiff-4e6c94bfd678c59b66cd39cef53193ed83a17d08.tar.gz

Downloaded from https://android.googlesource.com/platform/external/jdiff/+/4e6c94bfd678c59b66cd39cef53193ed83a17d08

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution



### Git project "platform/external/jhead":

File jhead-426377d9ce95606bac741d99b5b0a3e2038924fe.tar.gz

Downloaded from https://android.googlesource.com/platform/external/jhead/+/426377d9ce95606bac741d99b5b0a3e2038924fe

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/jpeg":

File jpeg-d9bb1510bee7d9bf2a0f2699c647a65e67ab9cf8.tar.gz

Downloaded from https://android.googlesource.com/platform/external/jpeg/+/d9bb1510bee7d9bf2a0f2699c647a65e67ab9cf8

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/libffi":

File libffi-056e203a7aec4c87c077192ad776b532a3d0305f.tar.gz

Downloaded from https://android.googlesource.com/platform/external/libffi/+/056e203a7aec4c87c077192ad776b532a3d0305f

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution

### Git project "platform/external/libpcap":

File libpcap-858aa678df9736fefabc0671973c0f58dc246f91.tar.gz

Downloaded from https://android.googlesource.com/platform/external/libpcap/+/858aa678df9736fefabc0671973c0f58dc246f91

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/libpng":

File libpng-368f3c41d0e7f802a92a59a342c6ae37d212743d.tar.gz

Downloaded from https://android.googlesource.com/platform/external/libpng/+/368f3c41d0e7f802a92a59a342c6ae37d212743d

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/libxml2":

File libxml2-6e8825d5c6462dd394226dbd7b193f95b40c4f22.tar.gz

Downloaded from https://android.googlesource.com/platform/external/libxml2/+/6e8825d5c6462dd394226dbd7b193f95b40c4f22

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/netcat":

File netcat-446d5a68930e2dbab2a9b2ab7d9f4fd5a7bd7419.tar.gz

Downloaded from https://android.googlesource.com/platform/external/netcat/+/446d5a68930e2dbab2a9b2ab7d9f4fd5a7bd7419

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/netperf":

File netperf-95f43f4cdc93396b513e017be8d1c7cc5bf846ef.tar.gz

Downloaded from https://android.googlesource.com/platform/external/netperf/+/95f43f4cdc93396b513e017be8d1c7cc5bf846ef

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/neven":

File neven-30957f56b33a18c5a4af787f25b9f145f2803634.tar.gz

Downloaded from https://android.googlesource.com/platform/external/neven/+/30957f56b33a18c5a4af787f25b9f145f2803634

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/opencore":

File opencore-e4e1fdb450347fcb33f19e8a5c2f3f2cb2645967.tar.gz

Downloaded from https://android.googlesource.com/platform/external/opencore/+/e4e1fdb450347fcb33f19e8a5c2f3f2cb2645967

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/openssl":

File openssl-f48372ded3bb76c2598392aa58abe6e2eb7432d2.tar.gz

Downloaded from https://android.googlesource.com/platform/external/openssl/+/f48372ded3bb76c2598392aa58abe6e2eb7432d2

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/oprofile":

File oprofile-48ae5fc270ea3bbb965b4bd07cb1691a5c115642.tar.gz

Downloaded from https://android.googlesource.com/platform/external/oprofile/+/48ae5fc270ea3bbb965b4bd07cb1691a5c115642

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/ping":

File ping-315013e18c06adca06f23be9bc6556fbd22f0c87.tar.gz

Downloaded from https://android.googlesource.com/platform/external/ping/+/315013e18c06adca06f23be9bc6556fbd22f0c87

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/ppp":

File ppp-dab68864983c4a0c6ef9e6d7e5834472c4c75f9c.tar.gz

Downloaded from https://android.googlesource.com/platform/external/ppp/+/dab68864983c4a0c6ef9e6d7e5834472c4c75f9c

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/protobuf":

File protobuf-35be73bfebdd5cf76922b2a44b15ebbbeaa8d079.tar.gz

Downloaded from https://android.googlesource.com/platform/external/protobuf/+/35be73bfebdd5cf76922b2a44b15ebbbeaa8d079

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/qemu":

File qemu-55f4e4a5ec657a017e3bf75299ad71fd1c968dd3.tar.gz

Downloaded from https://android.googlesource.com/platform/external/qemu/+/55f4e4a5ec657a017e3bf75299ad71fd1c968dd3

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/safe-iop":

File safe-iop-a09f917d93140479fd7964892dd38d3a86c42b7a.tar.gz

Downloaded from https://android.googlesource.com/platform/external/safe-iop/+/a09f917d93140479fd7964892dd38d3a86c42b7a

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/skia":

File skia-262917823441f183fa67aa63b9c0ec4e52cce4c3.tar.gz

Downloaded from https://android.googlesource.com/platform/external/skia/+/262917823441f183fa67aa63b9c0ec4e52cce4c3

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/sonivox":

File sonivox-e442bb7cd6a085b33a4dd52c0e20a157ada7feb1.tar.gz

Downloaded from https://android.googlesource.com/platform/external/sonivox/+/e442bb7cd6a085b33a4dd52c0e20a157ada7feb1

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/sqlite":

File sqlite-6005ac625aa553fe461b363385a8ed4a3c217a1f.tar.gz

Downloaded from https://android.googlesource.com/platform/external/sqlite/+/6005ac625aa553fe461b363385a8ed4a3c217a1f

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/srec":

File srec-8fc5a7f51e62cb4ae44a27bdf4176d04adc80ede.tar.gz

Downloaded from https://android.googlesource.com/platform/external/srec/+/8fc5a7f51e62cb4ae44a27bdf4176d04adc80ede

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/strace":

File strace-4a3ec90c3aa1cecc489f6fd19d785c6473ee8164.tar.gz

Downloaded from https://android.googlesource.com/platform/external/strace/+/4a3ec90c3aa1cecc489f6fd19d785c6473ee8164

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/tagsoup":

File tagsoup-926d907a2fb69573f1c6337f064645dde18b1e5e.tar.gz

Downloaded from https://android.googlesource.com/platform/external/tagsoup/+/926d907a2fb69573f1c6337f064645dde18b1e5e

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/tcpdump":

File tcpdump-9799c4b4d38c4aa2acc7ec7d593983bd178e49f6.tar.gz

Downloaded from https://android.googlesource.com/platform/external/tcpdump/+/9799c4b4d38c4aa2acc7ec7d593983bd178e49f6

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/tinyxml":

File tinyxml-09457b6e6c51b981b61a99a2157e0b3dd4bea444.tar.gz

Downloaded from https://android.googlesource.com/platform/external/tinyxml/+/09457b6e6c51b981b61a99a2157e0b3dd4bea444

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/tremor":

File tremor-28350ca441529b0f17844a39e2fc1b63ea7d83ef.tar.gz

Downloaded from https://android.googlesource.com/platform/external/tremor/+/28350ca441529b0f17844a39e2fc1b63ea7d83ef

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/webkit":

File webkit-9364f22aed35e1a1e9d07c121510f80be3ab0502.tar.gz

Downloaded from https://android.googlesource.com/platform/external/webkit/+/9364f22aed35e1a1e9d07c121510f80be3ab0502

Committer: The Android Open Source Project <initial-contribution@android.com>

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/wpa_supplicant":

File wpa_supplicant-ef98df019e941b9a51686e89495c16b4ead23140.tar.gz

Downloaded from https://android.googlesource.com/platform/external/wpa_supplicant/+/ef98df019e941b9a51686e89495c16b4ead23140

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/yaffs2":

File yaffs2-85ff57da47aaa93dc0018940cbd6b1f923664b46.tar.gz

Downloaded from https://android.googlesource.com/platform/external/yaffs2/+/85ff57da47aaa93dc0018940cbd6b1f923664b46

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/external/zlib":

File zlib-edc3fb3b9f9250ceacaf07a83beb5dde02807f9c.tar.gz

Downloaded from https://android.googlesource.com/platform/external/zlib/+/edc3fb3b9f9250ceacaf07a83beb5dde02807f9c

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/frameworks/base":  Core Android app framework libraries

File base-54b6cfa9a9e5b861a9930af873580d6dc20f773c.tar.gz

Downloaded from https://android.googlesource.com/platform/frameworks/base/+/54b6cfa9a9e5b861a9930af873580d6dc20f773c

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/frameworks/opt/com.google.android":

File com.google.android-19915d13a476d1dc054db396c1c755507fa43a42.tar.gz

Downloaded from https://android.googlesource.com/platform/frameworks/opt/com.google.android/+/19915d13a476d1dc054db396c1c755507fa43a42

Committer: The Android Open Source Project <initial-contribution@android.com>

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/frameworks/opt/com.google.android.googlelogin":

File com.google.android.googlelogin-844632d1ca7c49ad62b8a09f7d735712c416e3d3.tar.gz

Downloaded from https://android.googlesource.com/platform/frameworks/opt/com.google.android.googlelogin/+/844632d1ca7c49ad62b8a09f7d735712c416e3d3

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/frameworks/policies/base": Framework configuration policies

File base-58096b60fc111564c663d685d3b147ea4a5f3832.tar.gz

Downloaded from https://android.googlesource.com/platform/frameworks/policies/base/+/58096b60fc111564c663d685d3b147ea4a5f3832

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/hardware/libhardware": Hardware abstraction library

File libhardware-d6054a36475b5ff502b4af78f7d272a713c1a8e7.tar.gz

Downloaded from https://android.googlesource.com/platform/hardware/libhardware/+/d6054a36475b5ff502b4af78f7d272a713c1a8e7

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/hardware/ril": Radio interface layer

File ril-dbbb392e15b5ace6f19e76c49c80ea14292e8a4d.tar.gz

Downloaded from https://android.googlesource.com/platform/hardware/ril/+/dbbb392e15b5ace6f19e76c49c80ea14292e8a4d

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "kernel/msm": contains the linux kernel  v2.6.25 open source files the msm7k SoCs (if you want to rebuild the kernel)

Note: the firat Android phone "HTC Dream" has CPU "MSM7201A" by Qualcomm, so it's part of the "msm" family.

File msm-4b119e21d0c66c22e8ca03df05d9de623d0eb50f.tar.gz

Downloaded from https://android.googlesource.com/kernel/msm/+/4b119e21d0c66c22e8ca03df05d9de623d0eb50f

Committer: Linus Torvalds <torvalds@linux-foundation.org>

Commit date: Wed Apr 16 19:49:44 2008 -0700

Description: Linux 2.6.25

File linux-2.6.25.zip should be same or similar to the above.
Downloaded from  https://github.com/torvalds/linux/archive/refs/tags/v2.6.25.zip 

Also, file linux-2.6.25-android-1.0_r1.tar.gz can be found at https://web.archive.org/web/20081207064316/http://code.google.com/p/android/downloads/list
I haven't included it here because I am unsure about its copyrights.

Note: I haven't tried to do a folder diff of these 3 archive files to see how do they differ.


### Git project "platform/packages/apps/AlarmClock":

File AlarmClock-291e1a50b41a6ae47eddb1713dc99d22f96d0c9f.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/AlarmClock/+/291e1a50b41a6ae47eddb1713dc99d22f96d0c9f

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Browser":

File Browser-ba6d7b853c32ad6c3be26c443daa61f322bcfdc2.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Browser/+/ba6d7b853c32ad6c3be26c443daa61f322bcfdc2

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Calculator":

File Calculator-979004c651c1dc2327c4d74688cbaa5cbb9f08e1.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Calculator/+/979004c651c1dc2327c4d74688cbaa5cbb9f08e1

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Calendar":

File Calendar-a390cbfd25a5f3b2f002df725b7580bc78bd9edf.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Calendar/+/a390cbfd25a5f3b2f002df725b7580bc78bd9edf

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Camera":

File Camera-1d4c75065966c4f6f56900e31f655bfd1b334435.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Camera/+/1d4c75065966c4f6f56900e31f655bfd1b334435

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Contacts":

File Contacts-5dc3b4f80f38c0d48601f66c2c0e551474a7f8ad.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Contacts/+/5dc3b4f80f38c0d48601f66c2c0e551474a7f8ad

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Email":

File Email-8978aac1977408b05e386ae846c30920c7faa0a6.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Email/+/8978aac1977408b05e386ae846c30920c7faa0a6

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/GoogleSearch":

File GoogleSearch-c398e48938ffaa5ff8db0de81a54a4952e26394f.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/GoogleSearch/+/c398e48938ffaa5ff8db0de81a54a4952e26394f

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/HTMLViewer":

File HTMLViewer-dbdb2a036901f82d3bb27e35a8140206da2328dd.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/HTMLViewer/+/dbdb2a036901f82d3bb27e35a8140206da2328dd

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/IM":

File IM-4879f9aa9a3ba8ea89fe31f8d765c4908d4fd53a.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/IM/+/4879f9aa9a3ba8ea89fe31f8d765c4908d4fd53a

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Launcher":

File Launcher-c8f00b61c600927ab404c84686d4472e9b527976.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Launcher/+/c8f00b61c600927ab404c84686d4472e9b527976

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Mms":

File Mms-8eed706474910ccb978acda03e85d3261037da6e.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Mms/+/8eed706474910ccb978acda03e85d3261037da6e

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Music":

File Music-6cb8bc92e0ca524a76a6fa3f6814b43ea9a3b30d.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Music/+/6cb8bc92e0ca524a76a6fa3f6814b43ea9a3b30d

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/PackageInstaller":

File PackageInstaller-088073e6787fca4bfc68d6b04a5e887a03faf745.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/PackageInstaller/+/088073e6787fca4bfc68d6b04a5e887a03faf745

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution

### Git project "platform/packages/apps/Phone":

File Phone-abc47110c17fa8e8cb6161bc045e87f31eeb7a1c.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Phone/+/abc47110c17fa8e8cb6161bc045e87f31eeb7a1c

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Settings":

File Settings-de2d9f5f109265873196f1615e1f3546b114aaa7.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Settings/+/de2d9f5f109265873196f1615e1f3546b114aaa7

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/SoundRecorder":

File SoundRecorder-e2118f54af4c5215bd988979769e383292b9c9cb.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/SoundRecorder/+/e2118f54af4c5215bd988979769e383292b9c9cb

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Stk":

File Stk-e405ce157d5bfb44efa33a314ae08d543bc9d39e.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Stk/+/e405ce157d5bfb44efa33a314ae08d543bc9d39e

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Sync":

File Sync-79d30fe428c6dae46ae66afeb9d5c5f6ae34ddeb.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Sync/+/79d30fe428c6dae46ae66afeb9d5c5f6ae34ddeb

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/Updater":

File Updater-5fad77410b4e940237533bb8a0d306db36be0a23.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/apps/Updater/+/5fad77410b4e940237533bb8a0d306db36be0a23

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/apps/VoiceDialer":

File VoiceDialer-22464da53983813d22e37d9656e8cbd7809e9ebf.tar.gz 

Downloaded from https://android.googlesource.com/platform/packages/apps/VoiceDialer/+/22464da53983813d22e37d9656e8cbd7809e9ebf

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/CalendarProvider":

File CalendarProvider-b558dececce20291e0a0195a4bd9835f4a8a1918.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/CalendarProvider/+/b558dececce20291e0a0195a4bd9835f4a8a1918

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/ContactsProvider":

File ContactsProvider-0f58cfe01bb0f491330f7dcf85d54d0081459b57.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/ContactsProvider/+/0f58cfe01bb0f491330f7dcf85d54d0081459b57

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/DownloadProvider":

File DownloadProvider-57f55b3cb4f7e4136cde8d1ea12c1e70ec903362.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/DownloadProvider/+/57f55b3cb4f7e4136cde8d1ea12c1e70ec903362

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/DrmProvider":

File DrmProvider-6b8295c9350c603bdd930a29a877c8e95f4641ac.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/DrmProvider/+/6b8295c9350c603bdd930a29a877c8e95f4641ac

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/GoogleContactsProvider":

File GoogleContactsProvider-7251cb2492beceb08520bade25df701508246914.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/GoogleContactsProvider/+/7251cb2492beceb08520bade25df701508246914

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/GoogleSubscribedFeedsProvider":

File GoogleSubscribedFeedsProvider-f0d44cd75cfa07df3c9162bc2a03884c21a7fb8f.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/GoogleSubscribedFeedsProvider/+/f0d44cd75cfa07df3c9162bc2a03884c21a7fb8f

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/ImProvider":

File ImProvider-ef4989eb3bd594f384dd24ac3b2e7e13e180a026.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/ImProvider/+/ef4989eb3bd594f384dd24ac3b2e7e13e180a026

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/MediaProvider":

File MediaProvider-b80ba9251102fc785a5f231f41a61af1781723a2.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/MediaProvider/+/b80ba9251102fc785a5f231f41a61af1781723a2

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/packages/providers/TelephonyProvider":

File TelephonyProvider-15fe736a6429ed6e4cc0138ce88b241807af207e.tar.gz

Downloaded from https://android.googlesource.com/platform/packages/providers/TelephonyProvider/+/15fe736a6429ed6e4cc0138ce88b241807af207e

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/prebuilt": Binaries to support Linux and Mac OS builds

File prebuilt-e7214a75e616f54c5de3b38bfceae11ee5f1b9eb.tar.gz

Downloaded from https://android.googlesource.com/platform/prebuilt/+/e7214a75e616f54c5de3b38bfceae11ee5f1b9eb

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/system/bluetooth":

File bluetooth-6c2d13d0c3a4505fdac56ae8d537a68218e072f1.tar.gz

Downloaded from https://android.googlesource.com/platform/system/bluetooth/+/6c2d13d0c3a4505fdac56ae8d537a68218e072f1

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/system/core": Minimal bootable environment

File core-4f6e8d7a00cbeda1e70cc15be9c4af1018bdad53.tar.gz

Downloaded from https://android.googlesource.com/platform/system/core/+/4f6e8d7a00cbeda1e70cc15be9c4af1018bdad53

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/system/extras": Low-level debugging/inspection tools

File extras-7341494707810f709855ea85ce03a8ec3ac8dbaf.tar.gz

Downloaded from https://android.googlesource.com/platform/system/extras/+/7341494707810f709855ea85ce03a8ec3ac8dbaf

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/system/wlan/ti": TI 1251 WLAN driver and tools

File ti-607e8a019b921eee008cd1e9ffc132318fabce7f.tar.gz

Downloaded from https://android.googlesource.com/platform/system/wlan/ti/+/607e8a019b921eee008cd1e9ffc132318fabce7f

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 21 07:00:00 2008 -0700

Description: Initial Contribution


### Git project "platform/vendor/htc/dream-open": build configuration for the Dream (aka G1, Android Dev Phone 1) hardware

File dream-open-419383f1193353baf5d3fae523e632363ee69637.tar.gz

Downloaded from https://android.googlesource.com/platform/vendor/htc/dream-open/+/419383f1193353baf5d3fae523e632363ee69637

Committer: Brian Swetland <swetland@google.com>

Commit date: Thu Oct 23 18:12:49 2008 -0700

Description: initial commit

Also, a newer file with more "stuff": dream-open-e3868b58332ab687e3d7225a04db4022572762e8.tar.gz

Downloaded from https://android.googlesource.com/platform/vendor/htc/dream-open/+/e3868b58332ab687e3d7225a04db4022572762e8

Committer: Iliyan Malchev <malchev@google.com>

Commit date: Wed Nov 12 18:54:28 2008 -0800

Description: add proprietary camera library to the extract script Signed-off-by: Iliyan Malchev <malchev@google.com>

I believe that this Git project was initially named "vendor/htc/dream".
See more at https://web.archive.org/web/20090228161022/https://source.android.com/documentation/building-for-dream 


### Git project "platform/hardware/msm7k": specific support for the MSM7K SoCs

File msm7k-a3a947cc7e1bfaf7b5cfc85b71f602edf562836d.tar.gz

Downloaded from https://android.googlesource.com/platform/hardware/msm7k/+/a3a947cc7e1bfaf7b5cfc85b71f602edf562836d

Committer: Brian Swetland <swetland@google.com>

Commit date: Tue Oct 28 21:53:33 2008 -0700

Description: msm7k hardware glue, initial checkin: libaudio

Also, a newer archive with more "stuff": msm7k-040da078eb98745efe4b3f05ad72e61c66ba70b5.tar.gz

Downloaded from https://android.googlesource.com/platform/hardware/msm7k/+/040da078eb98745efe4b3f05ad72e61c66ba70b5

Committer: Iliyan Malchev <malchev@google.com>

Commit date: Wed Nov 12 17:27:52 2008 -0800

Description: user-space RPC library Signed-off-by: Iliyan Malchev <malchev@google.com>

See more at https://web.archive.org/web/20090228161022/https://source.android.com/documentation/building-for-dream 


### Git project "git-repo": contains the "repo" python script that orchestrates the source code download

File git-repo-cf31fe9b4fb650b27e19f5d7ee7297e383660caf.tar.gz

Downloaded from https://gerrit.googlesource.com/git-repo/+/refs/tags/v1.0

Committer: The Android Open Source Project <initial-contribution@android.com>	

Commit date: Tue Oct 28 21:53:33 2008 -0700

Description: Initial Contribution



## Finally, here is the SHA-1 checksum of each file:

```
sha1sum *
463aba59bcb7ba63b9e1375ec4bffbc29da78fb7  aes-045e5c3c0c0154d54e7abd95bf6505ddfff27dee.tar.gz
7b91b4940a45f82e0466cc8ed2b2491710e0b3b6  apache-http-417f3b92ba4549b2f22340e3107d869d2b9c5bb8.tar.gz
... INCOMPLETE ...
```

As we can see, the long gibberrish in each file name is not a SHA-1 sum; it is the "commit id".

## That's all, folks :)
