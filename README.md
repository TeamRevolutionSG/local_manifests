Local Manifests Repository (Android Build Guide)
==============

This repository is utilized for building for the devices under Team Revolution SG.

| Supported Devices
|:-------------------------
| Sony Xperia SP
| 

Getting Started
---------------
To get started with building from Team Revolution sources, you are required to be
familiar with [Git and Repo](http://source.android.com/source/version-control.html).

How To Build a ROM for your device from TeamRevolution Sources- Tutorial
--------
### Build Environment

- Tested and Working on any version of Ubuntu - 14.04,14.10,15.04 (64-bit)
- Any other distribution based of the Ubuntu Distro such as Lubuntu, Xubuntu and etc.
- Any form of Terminal
- Decent hardware (minimum of at least a dual core CPU and 4 GB of RAM)
- A storage unit of any kind (We recommend utilizing SSDs as Mechanical HDDs slow down the build proccess drastically and the minimum storage size is 70GB. Having more will be useful with CCache[More on that later])
- Required Packages should have been installed

### Required Packages
##### Simply copy and paste this in a terminal window:
[Hint: This command updates the Ubuntu Packages List (Install Listing) and install the required version of Java]

     $ sudo apt-get install openjdk-7-jdk

### Let that install and then proceed.

### More copy and paste:
[Hint: Running this command installs the other required packages to build android]

     $ sudo apt-get update && sudo apt-get install git-core gnupg flex bison gperf libsdl1.2-dev libesd0-dev libwxgtk2.8-dev squashfs-tools build-essential zip curl libncurses5-dev zlib1g-dev openjdk-6-jre openjdk-6-jdk pngcrush schedtool libxml2 libxml2-utils xsltproc lzop libc6-dev schedtool g++-multilib lib32z1-dev lib32ncurses5-dev lib32readline-gplv2-dev gcc-multilib

### Getting the Source
- Making required directories
- Obtaining the repo binary
- Adding repo binary to your path
- Giving the repo binary proper permissions
- Initializing an empty repo
- Syncing the repo

Alright, so now we’re getting there. I have outlined the basics of what we’re about to do and broke them down as I know them. This is all pretty much going to be copy/paste so it’ll be fairly difficult to screw this up :)

##### Make directory for the repo binary

      $ mkdir ~/bin

##### Add directory for the repo binary to its path

      $ PATH=~/bin:$PATH

##### Downloading repo binary and placing it in the proper directory

      $ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

##### Giving the repo binary the proper permissions

      $ chmod a+x ~/bin/repo

##### Then, follow the directions stated by the ROM's platform manifest

##### Downloading TeamRevolution Source Code

      $  cd <to the source code folder which should be empty except for the .repo folder>
      $  source build/envsetup.sh
      $  cd .repo
      $  git clone https://github.com/TeamRevolutionSG/local_manifests.git -b <either cyanogenmod or omni>
      $  croot

##### Syncing the source
[Hint: This might take a long time as the source is about 13GB+]

      $  repo sync

###Building the ROM
- Preparing Required Binaries and Device Drivers
- Setting Up CCache (Optional)
- Building the ROM

Congratulations on the succesfull build initialization! Now, we shall go ahead and prepare to build for your device!

##### Preparing the ROM for devices
- Follow the AOSP Porting Instructions stated here to prepare the proprietary files for building for your device: (http://xda-university.com/as-a-developer/porting-aosp-roms-using-source-code)

##### Setting Up CCache
- CCache is a method of utilizing a specified storage space to speed up building. It can be referred to as the same caching your android device does to speed up application and system boot times. In this case, CCache will help build the ROM faster than standard build times (Able to cut-down 50% of time taken to build).
- To set up CCache, follow the following:


        $ echo "export USE_CCACHE=1" >> ~/.bashrc
      
        $ ~/<source code folder>/prebuilts/misc/linux-x86/ccache/ccache -M 50G

     -M 50G
The number before the letter G at the end specifies the amount of space CCache can use in your storage unit. As such, ensure that not too much of space is specified as this might result in unexpected errors although, the more storage you have, its recommended to have more CCache as it will decrease the build times. Most efficient build systems are able to utilize CCache to about 120G or more.

##### To build the ROM

      $ cd ~/<source code folder>
      $ . build/envsetup.sh && brunch <device>

##### Obtaining the zip created from the build process
To get the zip file that has been built, navigate to the following directory and find for the zip file:

      $ cd ~/<source code folder>/out/target/product/<devicename>/
