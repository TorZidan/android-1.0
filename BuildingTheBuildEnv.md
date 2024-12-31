# Building the Build Environment

In this codelab I will guide you thrugh the setup of a build environemnt where you can build the Android 1.0 project.

## Create a VM (Virtual Machine) in Oracle VirtualBox that runs Ubuntu v10.04.4 LTS 32-bit OS.

Obviously, this is just one way to do this. You can use any other VM software, or perhaps you can install Ubuntu v10.04 32-bit as "bare metal" OS on your PC. Or you can use some other old Linux distribution. Or you can find a preinstalled "image" that you can launch on Amazon, Google or Microsoft cloud.

The original instructions can be found at https://web.archive.org/web/20081022180011/http://source.android.com/download. In there, they recommend using Ubuntu 6.06. I tried installing it, but I could not get the "apt-get" update system to work; perhaps you can? As you can see below, we need to install quite a lot of packages through "apt-get". 

Why not use a recent, modern OS? I find that to be a lost battle: as new OS releases come out every year, the instructions here would need to be updated, which would end up in one huge mess.

Will the instructions here work foreverandeverandever? No. Most likely one day Ubuntu will cease the "apt" support for Ubuntu 10.04, and the instructions below will fail. Or the future VirtualBox VM software versions will no-longer run properly the Ubuntu 10 "guest" OS. 

"Can I skip all these installation steps and get from somewhere a VM file that is fully setup, and I would just boot it up on my PC using VirtuaBox?" No. I could share my file, but am not sure about violating any copyrights. And you should have security converns about downloading VM images and running them on your PC; in theory, they may have unwelcome "trojan" software that tries to hack your PC and everything else on your local network.

So let's proceed:

1. Download and install the latest version of Oracle VirtualBox from https://www.virtualbox.org/ on your favorite operating system. I am running mine on Windows 10. You will need a PC with at-least 8 GB of RAM and ~50 GB of free disk space. Launch Oracle VirtualBox.

1. Download the Ubuntu v10.04 32-bit installation ISO file `ubuntu-10.04.4-desktop-i386.iso` from https://old-releases.ubuntu.com/releases/10.04.0/ . Note: the max RAM (addressable space) for any 32-bit OS is 4 GB, which is plenty for our purposes. Note: a 32-bit OS runs just fine on 64-bit processors.
   
1. In Virtual Box, choose "Machine -> New", choose "base memory" of 4 GB , "1" Processors, "50 GB" of virtual hard disk size, and go through the pain of launching the Ubuntu v10.04 installer from the ISO file and then follow the Ubuntu installation instructions. For me, the Ubuntu installation screens were partially off-screen, so I could not see the mouse pointer to click on "Next", etc. I had to use the "Tab" button to navingate on these windows, and hit "Enter" at the right place. Choose your favorite username (I chose "android") and a password.
   
1. Once the installation is complete:
    * Shut down the Ubuntu VM, then make sure that in the VM settings we have given enough Video RAM (I gave it 64 MB), and then launch the Ubuntu VM and login with yout chosen username/pwd.
    * Make sure the menu item Devices->Shared Clipboard is set to "Bidirectional".
    * Make sure under menu item Devices->Network the option "Connect Network Adapter" is checked.
    * Under the "View" menu, make sure the "Auto resize guest display" is checked.
    * In Ubuntu, under System->Preferences->Monitors choose a comfortable screen size, e.g. 1600x1200 pixels. The VM window should auto-resize to that much-needed bigger size. Nice.

1. In Ubuntu: fix the URL location of the package updates, so that we can download and install packages via `sudo apt-get install ....`:

    ```
    sudo sed -i -e 's/archive.ubuntu.com\|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
    sudo sed -i -e 's/us.old-releases.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
    ```

    Why are we doing this? 
    Ubuntu 10.04 LTS was released in 2010. LTS (Long Term Support) releases are supported for 5 years. Once support is up, the repository is moved to another server.
    See https://smyl.es/how-to-fix-ubuntudebian-apt-get-404-not-found-package-repository-errors-saucy-raring-quantal-oneiric-natty/ for more info.

    Note: This works of 2022, but don't know for how long...

1. All commands from here-on should be run in the Ubuntu VM, in a "terminal" window. Run a `sudo apt-get update` . It should work fine, and it should download "stuff" and should update your system packages to their latest versions for Ubuntu 10.04 LTS.

1. Install the "VirtualBox" guest utilities in Ubuntu, which provide the glue for "copy/paste" support from/to your main OS and the "guest" Ubuntu OS: `sudo apt-get install virtualbox-ose-guest-utils virtualbox-ose-guest-x11 virtualbox-ose-guest-dkms`.

    Note: One of it's features is to be able to access folders on your main OS from within Ubuntu. I never managed to get it to work. Most likely these "guest utils" (which are circa-2010) no-longer work well with the latest version of VirtualBox. Oh, well. Would have been nice if it worked.

1. Install a lot of "stuff":
     * `sudo apt-get install linux-headers-2.6.32-74 linux-headers-2.6.32-74-generic`
     * `sudo apt-get install flex bison gperf libsdl-dev libesd0-dev libwxgtk2.6-dev build-essential zip curl zlib1g-dev`
     * `sudo apt-get install libwxgtk2.6-dbg libwxbase2.6-dbg libwxgtk2.6-0 libwxgtk2.6-dev libwxgtk2.6-dbg libwxbase2.6-0 wx2.6-headers`
     * `sudo apt-get install g++-4.1 g++-4.1-multilib libstdc++6-4.1-dbg libstdc++6-4.1-doc libstdc++6-4.1-dev`
     * `sudo apt-get install  gcc-4.1 gcc-4.1-base cpp-4.1 gcc-4.1-doc gcc-4.1-multilib gcc-4.1-locales libmudflap0-dev` 
     * `sudo apt-get install valgrind`
     * `sudo apt-get install git-core`
     * `sudo apt-get install openssl zlib1g-dev gettext libcurl4-openssl-dev`

1. Install Java and JDK 1.5:
      * On a modern PC, download file `jdk-1_5_0_22-linux-i586.bin` from https://www.oracle.com/java/technologies/java-archive-javase5-downloads.html . You will need to create an Oracle.com account (it's free) and go through the pain of downloading this file. It ain't easy, but possible, I promise.
      * Transfer file `jdk-1_5_0_22-linux-i586.bin` to the Ubuntu VM, into your "home" folder. See a section below for how to transfer files from your PC to the VM.
      * Run these commands:
        ```
        cd ~ && chmod +x jdk-1_5_0_22-linux-i586.bin && mkdir java && cd java
        ../jdk-1_5_0_22-linux-i586.bin
            ... then scroll to the prompt, type "yes", enter. It will extract the Java files in subfoldfer `jdk1.5.0_22`.
        ```
1. Configure wxWidgets:
      * Run these commands:
        
       ```
       sudo update-alternatives --config wx-config
          ... then choose the number in front of "/usr/lib/wx/config/gtk2-unicode-release-2.6"
       ```

1. How can I transfer files from my PC to the "guest" Ubuntu OS and back? As I said above, there is a feature that enables Ubuntu to "see" a folder on your PC, but I could not get it to work. So I could try "ftp" or "sftp", but I went for a simpler approach: Use a small (e.g. 8 GB) flash drive; format it on your PC with "FAT 32". Use it to transfer files in the following way: Once the drive is recognized in your main OS, copy files to it. Then go to the VM window, go to menu "Devices->USB", and click on the falsh drive devices. Virtual box will "unmount it" from your main OS and mount it in Ubuntu; here, open a File Explorer window, give it a few seconds, and the flash drive will appear in the left pane. Click on it and the files will show up in the right pane. Now you can copy files from/to it. Once done, use the same menu item to "unmount it". You will need to physically unplug the flash drive and plug it again to get it recognized again in your main OS.

1. This should do it. Have you fould an easier way to do any of these steps? Let me know by opening a "New Issue" here, on Github. Now proceed to [Buildding Android 1.0](BuildingIt.md). 
  
     
