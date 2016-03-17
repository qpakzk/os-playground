### Installing Pintos and running in QEMU

_host platform independent procedure_

_all versions as of 2016-03-09_

_thanks to [Surya Seetharaman](https://tssurya.wordpress.com/2014/08/16/installing-pintos-on-your-machine/) for his instructions_

* * *

#### Prerequisites

1. An installation as in [virtual-dev-env](https://github.com/ivogeorg/os-playground/blob/master/virtual-dev-env.md) or equivalent.

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

7. Run Pintos. This will a `qemu` window and run the _alarm-multiple_ test. Note that this **doesn't mean the test is passing**. It's just running.

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

```
cd src/threads/build
make check
```

_Note that some of the tests, especially the MLFQS ones, take long to run, since they need to timeout when the functionality they test is not implemented. Some of the tests pass right off the bat, but you might break them when you start work._
