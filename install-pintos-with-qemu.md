### Installing Pintos and running in QEMU

_as of 2016-03-07_

* * *

#### Install VirtualBox

1. Open the downloads directory http://download.virtualbox.org/virtualbox/.
2. As of this writing, the latest version is 5.0.16. Open http://download.virtualbox.org/virtualbox/5.0.16/.
3. Download the installation image for your platform. Install.
4. Also download the guest extensions ISO VBoxGuestAdditions_5.0.16.iso. It's the same for all platforms.

#### Create an Ubuntu virtual machine

1. Open the desktop download site http://www.ubuntu.com/download/desktop.
2. Download the latest 64-bit ISO image. As of this writing, this is LTS 14.04.4.
3. Open VirtualBox and create a new machine. Give it a name and select **Linux** and **Ubuntu 64-bit**.
4. Start the machine. When asked for the installation image, point to the ISO image you donwloaded and continue.
5. When asked to _try_ or _install_ Ubuntu, select _install_.
6. Create a username and password. Select _Log in automatically_.
7. All installation defaults should be fine. Restart the machine when done.

#### Some housekeeping

1. Install the Ubuntu updates. There is a green button with an A. Click on it, provide the password and let it install.
2. Open a terminal. Click on the topmost button on the left and start typing "termin...". Click on the Terminal app. When it opens, there will be a terminal button in the menu. Right-click and select "Lock to the tray". Next time you can open from there.

#### Install the guest additions

1. The virtual machine is called a _guest_. The extensions will give you, among other things, a resizeable display. The default resolution won't be useful for development. If you want, read more about them [here](https://www.virtualbox.org/manual/ch04.html).
2. Install the dynamic kernel module support (DKMS) framework. Execute the following commands:
   ```
   sudo apt-get update
   sudo apt-get upgrade
   sudo apt-get install dkms
  ```
3. Click on the small disk picture on the bottom bar of the virtual machine window. Load the _VBoxGuestAdditions_5.0.16.iso_ (downloaded earlier) into the disk drive. Ubuntu will recognize that you want to install the Guest Additions.
4. 

