# Building the Build Environment

In this codelab I will guide you thrugh the setup of a build environemnt where you can build the Android 1.0 project.

## Create a VM (Virtual Machine) in Oracle VirtualBox that runs Ubuntu v10.04.4 LTS 32-bit OS.

Obviously, this is just one way to do this. You can use any other VM software, or perhaps you can install Ubuntu v10.04 32-bit as "bare metal" OS on your PC. Or you can find a preinstalled "image" that you can launch on Amazon, Google or Microsoft cloud.

1. Download and install the latest version of Oracle VirtualBox from https://www.virtualbox.org/ on your favorite operating system. I am running mine on Windows 10. You will need a PC with at-least 8 GB of RAM and ~50 GB of free disk space. Launch Oracle VirtualBox

1. Download the Ubuntu v10.04 32-bit installation ISO file 'ubuntu-10.04.4-desktop-i386.iso' from https://old-releases.ubuntu.com/releases/10.04.0/ . Note: the max RAM (addressable space) for any 32-bit OS is 4 GB, which is plenty for our purposes.
   
1. In Virtual Box, choose "Machine -> New", choose "base memory" of 4 GB , "1" Processors, "50 GB" of virtual hard disk size, and go through the pain of launching the Ubuntu v10.04 installer from the ISO file and then follow the Ubuntu installation instructions. For me, the Ubuntu installation screens were partially off-screen, so I could not see the mouse pointer to click on "Next", etc. I had to use the "Tab" button to navingate on these windows, and hit "Enter" at the right place. Choose your favorite username (I chose "android") and a password.
   
1. Once the installation is complete:
    * Shut down the Ubuntu VM, make sure that in the VM properties we have given it enough Video RAM (I gave it 64 MB), and then launch the Ubuntu VM and login with yout chosen username/pwd.
    * Make sure in that in the VM properties we have given enough Video RAM (I gave it 64 MB)
    * Make sure Devices->Shared Clipboard is set to "Bidirectional.
    * Make sure under Devices->Network the option "Connect Network Adapter" is checked.
    * Under "View" menu, make sure the "Auto resize guest display" is checked.
    * In Ubuntu, under System->Preferences->Monitors choose a comfortable screen size, e.g. 1600x1200 pixels.

1. In Ubuntu: fix the URL location of the package updates, so that we can download and install packages via `sudo apt-get install ....`:

    ```
    sudo sed -i -e 's/archive.ubuntu.com\|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
    sudo sed -i -e 's/us.old-releases.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
    ```

    Why are we doing this? 
    Ubuntu 10.04 LTS was released in 2010. LTS (Long Term Support) releases are supported for 5 years. Once support is up, the repository is moved to another server.
    See https://smyl.es/how-to-fix-ubuntudebian-apt-get-404-not-found-package-repository-errors-saucy-raring-quantal-oneiric-natty/ for more info.

    Note: This works of 2022, but don't know for how long...

1. Do a `sudo apt-get update` . It should work fine, and it should update your system packages to their latest versions for for Ubuntu 10.04 LTS.

1. Install the "VirtualBox" guest utilities in Ubuntu, which provide the glue for "copy/paste" support from/to your main OS and the Ubuntu OS: `sudo apt-get install virtualbox-ose-guest-utils virtualbox-ose-guest-x11 virtualbox-ose-guest-dkms`.

    Note: One of it's features is to be able to access folders on your main OS from within Ubuntu. I never managed to get it to work. Most likely these "guest utils" (which are circa-2010) no-longer work well with the latest version of VirtualBox. Oh, well. Would have been nice if it worked.

1. Install a lot of "stuff":
     * `sudo apt-get install g++-4.1`
     * `sudo apt-get install g++-4.1-multilib libstdc++6-4.1-dbg libstdc++6-4.1-doc`
     * `sudo apt-get install gcc-4.1`
     * TO BE CONTINUED
  
     
