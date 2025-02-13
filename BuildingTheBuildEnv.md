# Building the Build Environment

In this codelab I will guide you thrugh the setup of a build environemnt where you can build the Android 1.0 project.

## Create a VM (Virtual Machine) in Oracle VirtualBox that runs Ubuntu v8.04.4 LTS 32-bit OS.

Obviously, this is just one way to do this. You can use any other VM software, or perhaps you can install Ubuntu 8.04 32-bit as "bare metal" OS on your PC. Or you can use some other old Linux distribution. Or you can find a preinstalled "image" that you can launch on Amazon, Google or Microsoft cloud.

The original instructions can be found at https://web.archive.org/web/20081022180011/http://source.android.com/download. In there, they recommend using Ubuntu 6.06. I tried installing it, but I could not get the Virtualbox guest additions software to work well, wich resulted in a lagging mouse pointer and low screen resolution.

Why not use a recent, modern Linux OS? I find that to be a lost battle: as new Linux (e.g. Ubuntu) OS releases come out every year, the instructions here would need to be updated, which would end up in one huge mess. The newer version of `gcc` and `g++` compilers are more strict and error out on this old codebase. Fixing these build errors would result in something that is no-longer Android 1.0. Installing old gcc compilers, libraries and toolchains on modern OS is not fun, either. But you are welcome to try!

Will the instructions here work foreverandeverandever? No. Most likely one day Ubuntu will cease the "apt" software update support for Ubuntu 8.04, and the instructions below will fail. Or the future VirtualBox VM Guest Additions software versions will no-longer run properly on the Ubuntu 8 "guest" OS, which will make it extremely painful to use (lagging, misplaced mouse cursor, low screen resolution, no way to transfer files to/from the VM host computer).

"Can I skip all these installation steps and find somewhere a VM file that is fully setup, and I would just boot it up on my PC using VirtuaBox?" Not a good idea. I could share my VM file, but am not sure about violating any copyrights. And you should have security concerns about downloading VM images and running them on your PC; in theory, they may have unwelcome "trojan" software that tries to hack your host PC and everything else on your local network.

So let's proceed:

1. Download and install the latest version of Oracle VirtualBox from https://www.virtualbox.org/ on your favorite operating system. In 2025, I am running version 7.1.4 on Windows 10. You will need a PC with at-least 8 GB of RAM and ~50 GB of free disk space. Once installed, launch Oracle VirtualBox.

1. Download the Ubuntu v8.04 32-bit installation ISO file `ubuntu-8.04-desktop-i386.iso` from [https://old-releases.ubuntu.com/releases/8.04.0/](https://old-releases.ubuntu.com/releases/8.04.0/) . Note: the max RAM (addressable space) for any 32-bit OS is 4 GB, which is plenty for our purposes. Note: a 32-bit OS runs just fine on all 64-bit processors from Intel and AMD.
   
1. In Virtual Box, choose "Machine -> New", choose "Base memory" of 4 GB , "1" Processors, "50 GB" of virtual hard disk size, and go through the pain of launching the Ubuntu v8.04 installer from the ISO file and then follow the Ubuntu installation instructions. For me, the Ubuntu installation screens were partially off-screen, so I could not see the mouse pointer to click on "Next", etc. I had to use the "Tab" button to navingate in these windows, and hit "Enter" at the right place. Choose your favorite username (I chose "android") and a password.
   
1. Once the installation is complete:
    * Shut down the Ubuntu VM, then go to the VM Settings, section "Display". Give it enough Video Memory (I gave it 64 MB); also, in the "Graphics Controller" Dropdown choose "VBoxSVGA". then launch the Ubuntu VM and login with yout chosen username/pwd.
    * Make sure the menu item Devices->Shared Clipboard is set to "Bidirectional" (Note: I cound never get copy/paste from/to the host and guest VM to work).
    * Make sure under menu item Devices->Network the option "Connect Network Adapter" is checked.
    * Under the "View" menu, make sure the "Auto resize guest display" is checked.
    * Restart the Ubuntu VM and login with the chosen username/password.

1. Install the "VirtualBox" guest additions software in Ubuntu:
    * In the running VM window's top menu bar, choose "Devices -> Insert Guest Additions CD Image". You will see a CD rom appear as an icon on the Ubuntu desktop. It will ask you if you want to run the software from it; choose no (instead,we will run it from the command line).
   * Open a terminal window and run: `sudo sh /media/cdrom0/VBoxLinuxAdditions.run`. It should succeed.
   * Note: This software is important in order to get a usable VM. It provides: copy/paste support from/to the guest OS and the Ubuntu VM (which never worked for me), support for file transfers from/to the host and the Ubuntu VM, non-lagging, accurate mouse cursor, video drivers that give you nice screen resolution, and more.
   * Restart the Ubuntu VM and login.

1. In the Ubuntu window's top menu, choose "System -> Preferences -> Screen Resolution". Choose a comfortable resolution depending on your monitor, e.g. 1600x1200. Apply and keep the settings. The Ubuntu VM screen should auto-resize to its new larger size (if not, just drag and resize it with the mouse). Much better.
   
1. The commands below are quite long and ideally you should copy/paste them into the Ubuntu VM command line window. However, given that copy/paste from/to the host OS and the Ubuntu VM does not work for me, I had to get creative to get the text on this web page to the Ubuntu VM:
    * Option 1 (recommended): Save the text from this web page into a text file on your PC. Then, in the Ubuntu VM wondow, from the top menu, choose "Machine -> File Manager". A file transfer window will open. In the lower right, type in your username and password and click "Open Session". Transfer the text file to the Ubuntu VM (e.g. into the home folder), and double-click on it in Ubuntu to open it with "Text Editor". Now you can select and copy text into the clipboard (via Ctrl+C) and then paste into the terminal window prompt with Ctrl+Shift+V.
    * Option 2. In the VM settings, you can "mount" a folder from your host OS to be "visible" in Ubuntu; do that for the folder that contains the text file. Then, in Ubuntu, navigate to the text file and double-click to open it in "Text Editor".
    * Option 3. If you have python 3 (or later) installed on your host OS, you can run an http server from the command line: `python -m http.server 8000`. Then, in Ubuntu, open Firefox and navigate to `http://<your host IP address>:8000/`. You will see all files and folders on your host (e.g. on your Windows C:\ drive). Navigat to the text file, and copy/paste text from this web page into the Ubuntu terminal command prompt.
    * Option 4: Use a small (e.g. 8 GB) flash drive; format it on your PC with "FAT 32". Use it to transfer files in the following way: Once the drive is recognized in your host OS, copy files to it. Then go to the Ubuntu VM window, in the top menu go to "Devices->USB", and click on the falsh drive devices. Virtual Box will "unmount it" from your main OS and mount it in Ubuntu; here, open a File Explorer window, give it a few seconds, and the flash drive will appear in the left pane. Click on it and the files will show up in the right pane. Now you can copy files from/to it. Once done, use the same menu item to "unmount it". You will need to physically unplug the flash drive and plug it again to get it recognized again in your main OS.
    * Note: Ubuntu 8 uses obsoleted SSL/HTTPS/TLS software and has some expired "trusted certificate authorities". This prevents you from viewing most web sites, including Github; also, most web sites no-longer support "http" (unencrypted communication) or "ftp" (unencrypted file transfer). Perhaps you can download and install the latest Chromium web browser? Just downloading the installation file from the web would be a major pain (hint: both `wget` and `curl` will fail with SSL erors).
   
1. In Ubuntu: fix the URL location of the Ubuntu software package updates, so that we can download and install packages via `sudo apt-get install ....`:

    ```
    sudo cp /etc/apt/sources.list /etc/apt/sources_original.list
    sudo sed -i -e 's/archive.ubuntu.com\|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
    sudo sed -i -e 's/us.old-releases.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
    ```

    Then restart the Ubuntu VM.

    Why are we doing this?  Ubuntu 8.04 LTS was released in 2008. LTS (Long Term Support) releases are supported for 5 years. Once support is up, the repository is moved to another server.
    See https://smyl.es/how-to-fix-ubuntudebian-apt-get-404-not-found-package-repository-errors-saucy-raring-quantal-oneiric-natty/ for more info. Note: This still works in 2025, but don't know for how long it will ...

1. In Ubuntu, from the top menu, go to "System-> Administration -> Update Manager, install all available updates (note: do not click on "Upgrade to Ubuntu 10"). %estart the Ubuntu VM again.

1. Install a lot of "stuff" by executing these commands in a "terminal" window in Ubuntu:
     * `sudo apt-get install flex`
     * `sudo apt-get install bison`
     * `sudo apt-get install gperf`
     * `sudo apt-get install libsdl-dev`
     * `sudo apt-get install libesd0-dev`
     * `sudo apt-get install libwxgtk2.6-dev`
     * `sudo apt-get install build-essential`
     * `sudo apt-get install curl`
     * `sudo apt-get install zlib1g-dev`
     * `sudo apt-get install libncurses5-dev`

1. Install Java and JDK 1.5:
      * On a modern PC, download file `jdk-1_5_0_22-linux-i586.bin` from https://www.oracle.com/java/technologies/java-archive-javase5-downloads.html . You will need to create an Oracle.com account (it's free) and go through the pain of downloading this file. It ain't easy, but possible, I promise.
      * Transfer file `jdk-1_5_0_22-linux-i586.bin` to the Ubuntu VM, into your "home" folder. See a section below for how to transfer files from your PC to the VM.
      * Run these commands:
        ```
        cd ~ && chmod +x jdk-1_5_0_22-linux-i586.bin && mkdir java && cd java
        ../jdk-1_5_0_22-linux-i586.bin
            ... then scroll to the prompt, type "yes", enter. It will extract the Java files in subfoldfer `jdk1.5.0_22`.
        ```

1. This should do it. Have you found an easier way to do any of these steps? Let me know by opening a "New Issue" here, on Github. Now proceed to [Buildding Android 1.0](StepsToBuild.md). 
  
     
