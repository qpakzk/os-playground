### Installing Pintos and running in QEMU

_host platform independent procedure_

_all versions as of 2016-03-08_

_thanks to [Surya Seetharaman](https://tssurya.wordpress.com/2014/08/16/installing-pintos-on-your-machine/) for his instructions_

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

3. Click on the small disk picture on the bottom bar of the virtual machine window. Click "Choose disk image" and select the _VBoxGuestAdditions_5.0.16.iso_ (downloaded earlier). Ubuntu will recognize that you want to install the Guest Additions. Agree to the installation.

4. After the installation, eject the disk from the left-hand menu bar, and restart the machine.

5. Now you can increase the resolution of the screen to something that is more convenient for development. Click the topmost button in the bar and start typing "displa...". Open the Displays app, adjust the screen resolution and click the (almost hidden) button to apply the changes. Either accept the resolution or change it again.

#### Some preparation

1. Open a terminal.

2. _(optional)_ Check if you have _cmake_ installed. This is a toolset for building and packaging software. If you want to know more, check out the [website](https://cmake.org/). If not, install it:

   ```
   which cmake
   sudo apt-get install cmake
   which cmake
   ```

3. Check if you have _git_ installed. This is a VCS. If you want to know more, check out the [website](https://git-scm.com/). We'll need it to fetch Pintos. If not, install it:
 
   ```
   which git
   sudo apt-get install git
   which git
   ```
   
4. Check if you have _QEMU_ installed. This is a virtualizer/**emu**lator. If you want to know more, check out the [website](http://wiki.qemu.org/Main_Page). We'll need it to run Pintos in. If not, install it:

   ```
   which qemu-system-x86_64
   sudo apt-get install qemu-system
   which qemu-system-x86_64
   ```
   
#### Download Pintos

1. Make a _git-repos_ directory in your home directory and clone the public Pintos repository inside it:

   ```
   cd
   mkdir git-repos
   cd git-repos
   git clone git://pintos-os.org/pintos-anon
   cd pintos-anon
   ```

2. Now you are in `$HOME/git-repos/pintos-anon` where `$HOME` is your home directory. To see the value of the environment variable `$HOME`:

   ```
   echo $HOME
   ```
   
3. We'll informally refer to this directory as `$PINTOS_ROOT` thought we don't have to have such an environment variable. All subsequent instructions assume that you start out in this directory. For me, this directory resolves to the absolute path `/home/ivogeorg/git-repos/pintos-anon`. Remember to expand it into the absolute path wherever it is referenced in a file.
   
#### Configure and build Pintos

1. Set the **GDBMACROS** variable in the file `$PINTOS_ROOT/src/utils/pintos-gdb` to `$PINTOS_ROOT/src/misc/gdb-macros`.

  1. Open an editor

     ```
     gedit src/utils/pintos-gdb
     ```

  2. Change Line 4 to `GDBMACROS=$PINTOS_ROOT/src/misc/gdb-macros`. Expand into absolute path. 

  3. Save the file.

2. Edit the file `$PINTOS_ROOT/src/utils/Makefile`.

  1. Open an editor

     ```
     gedit src/utils/Makefile
     ```
     
  2. Change Line 5 to `LDLIBS = -lm`. 

  3. Save the file.

3. Compile the utilities. You might get warnings. If only warnings, the build was successful.

   ```
   cd src/utils
   make
   cd ../..
   ```
   
4. Set simulator to `qemu` in the file `$PINTOS_ROOT/src/threads/Make.vars`.

  1. Open an editor

     ```
     gedit src/threads/Make.vars
     ```
     
  2. Change Line 7 (last line) to `SIMULATOR = --qemu`. 

  3. Save the file.

5. Compile the Pintos kernel.

   ```
   cd src/threads
   make
   cd ../..
   ```
   
6. Edit the file `$PINTOS_ROOT/src/utils/pintos`, which is a Perl script.

  1. Open an editor

     ```
     gedit src/utils/pintos
     ```
     
  2. Change Line 103 to `$sim = “qemu” if !defined $sim;` to use QEMU as the simulator. Preserve the indentation. 

  3. Change `kernel.bin` on Line 257 to `$KERNEL_ROOT/src/threads/build/kernel.bin`. Expand to absolute path.
  
  4. Change `qemu-system-i386` on Line 621 to `qemu-system-x86_64`.
  
  5. Save the file.

6. Edit the file `$PINTOS_ROOT/src/utils/Pintos.pm`, which contains Perl helper subroutines.

  1. Open an editor

     ```
     gedit src/utils/Pintos.pm
     ```
     
  2. Change `loader.bin` on Line 362 to `$KERNEL_ROOT/src/threads/build/loader.bin`. Expand to absolute path.
  
  5. Save the file.

7. Run Pintos. This will a `qemu` window and run the _alarm-multiple_ test. Note that this ~~won't pass~~ the test, just run it.

   ```
   cd src/utils
   pintos run alarm-multiple
   ```
   
#### A little bit of housekeeping

1. Add the `pintos` executable path to your $PATH environment variable.


  1. Open an editor

     ```
     gedit ~/.bashrc
     ```   
     
  2. Add the following line to the end of the file `export PATH=$PINTOS_ROOT/src/utils:$PATH`. Expand to absolute path.

  3. Save the file and restart the terminal. You can now run `pintos ... ...` from anywhere.
  

#### Run the tests for Project 1: Threads

1. Run the 
