### Installing Pintos and running in QEMU

_host platform independent procedure_
_linux user independent procedure for streamlined grading_

_all versions as of 2018-02-13_

* * *

#### Prerequisites

1. An installation as in [virtual-dev-env](https://github.com/ivogeorg/os-playground/blob/master/virtual-dev-env.md) or equivalent. Assuming a user called `pintos` with home directory `/home/pintos` (on Ubuntu). All the following commands are meant to be executed on the command line in a terminal window.

#### Download Pintos

1. The public Pintos repository is [here](http://pintos-os.org/cgi-bin/gitweb.cgi?p=pintos-anon;a=summary). Clone it to the home directory, giving it the name `pintos`.
   ```
   cd ~
   git clone git://pintos-os.org/pintos-anon pintos
   ```

2. Now you are in `$HOME/pintos` where `$HOME` is your home directory. This is `/home/pintos/pintos` if you followed the intallation instructions in [virtual-dev-env](https://github.com/ivogeorg/os-playground/blob/master/virtual-dev-env.md). To see the value of the environment variable `$HOME`:

   ```
   echo $HOME
   ```
   
3. We'll informally refer to this directory as `$PINTOS_ROOT` though we don't have to have such an environment variable. Paths in all the following instructions are relative to this directory. If you followed the installation instructions, this directory is the absolute path `/home/pintos/pintos`. Remember to expand it into the absolute path wherever it is referenced in a file or path variable.
   
#### Configure and build Pintos

1. Set the **GDBMACROS** variable in the file `$PINTOS_ROOT/src/utils/pintos-gdb` to `$PINTOS_ROOT/src/misc/gdb-macros`.

    1. Open an editor

       ```
       vim src/utils/pintos-gdb
       ```

    2. Change Line 4 to `GDBMACROS=$PINTOS_ROOT/src/misc/gdb-macros`. Expand into absolute path. 

    3. Save the file.

2. Edit the file `$PINTOS_ROOT/src/utils/Makefile`.

    1. Open an editor

       ```
       vim src/utils/Makefile
       ```
     
    2. Change Line 5 to `LDLIBS = -lm`. 

    3. Save the file.

3. Compile the utilities. You might get warnings. If only warnings, the build was successful.

   ```
   cd src/utils
   make
   ```
   
4. Set simulator to `qemu` in the file `$PINTOS_ROOT/src/threads/Make.vars`.

    1. Open an editor

       ```
       vim src/threads/Make.vars
       ```
     
    2. Change Line **7** (last line) to `SIMULATOR = --qemu`. 

    3. Save the file.

5. Compile the Pintos kernel.

   ```
   cd src/threads
   make
   ```
   
6. Edit the file `$PINTOS_ROOT/src/utils/pintos`, which is a Perl script.

    1. Open an editor

       ```
       vim src/utils/pintos
       ```
     
    2. Change line **103** to `$sim = “qemu” if !defined $sim;` to use QEMU as the simulator. Preserve the indentation. 

    3. Change `kernel.bin` on line **257** to `$PINTOS_ROOT/src/threads/build/kernel.bin`. Expand to absolute path.
  
    4. ~Change `qemu-system-i386` on line **621** to `qemu-system-x86_64`.~ _Runs fine with original setting_ `qemu-system-i386`.
  
    5. Save the file.

6. Edit the file `$PINTOS_ROOT/src/utils/Pintos.pm`, which contains Perl helper subroutines.

    1. Open an editor

       ```
       vim src/utils/Pintos.pm
       ```
     
    2. Change `loader.bin` on Line **362** to `$PINTOS_ROOT/src/threads/build/loader.bin`. Expand to absolute path.
  
    3. Save the file.

7. Run Pintos. The following will open a Qemu terminal window and run the _alarm-multiple_ test. Note that this **doesn't mean the test is passing**. It's just running. You can just close the Qemu terminal when the test execution completes.

   ```
   cd src/utils
   ./pintos run alarm-multiple
   ```
   
#### A little bit of housekeeping

1. Add the `pintos` executable path to your $PATH environment variable.

    1. Open an editor

       ```
       vim ~/.bashrc
       ```   
     
    2. Add the following line to the end of the file `export PATH=$PINTOS_ROOT/src/utils:$PATH`. Expand to absolute path. Reopen the terminal.

    3. Save the file and restart the terminal. You can now run `pintos ... ...` from anywhere.
  

#### Run the tests for Project 1: Threads

The following runs all tests one after the other with full output.

```
cd src/threads/build
make check VERBOSE=1
```

_Note that some of the tests, especially the MLFQS ones, take long to run, since they need to gather statistics. Some of the tests pass right off the bat, but you might break them when you start work._

#### Run the tests for Project 2: User Programs

_Note: Project 2 does not need any of the functionality implemented in Project 1. In particular, all threads are created with priority `PRI_DEFAULT` and the scheduler runs simple round-robin. So, if you passed all tests in Project 1, you can just continue working in your current install. Or, you can start with a new raw Pintos install._

1. Make sure you run a top-level clean (of `threads`) before you build for `userprog`.

```
cd ~/pintos
make clean
```

2. In the Perl script `src/utils/pintos`, change `kernel.bin` on line **257** to `/home/pintos/pintos/src/userprog/build/kernel.bin`.

3. In the Perl script `src/utils/Pintos.pm`, change `kernel.bin` on line **362** to `/home/pintos/pintos/src/userprog/build/loader.bin`.

4. Build the project.

```
cd src/utils
make
cd src/userprog
make
cd build
```

5. Create a filesystem disk for `userprog`. _(Assumes the kernel was built under `userprog/`. Similarly, for `vm` and `filesys`.)_

```
cd ~/pintos/src/userprog/build
pintos-mkdisk filesys.dsk --filesys-size=2
```

6. Format the disk with a filesystem partition. _(Assumes the kernel was built under `userprog/`. Similarly, for `vm` and `filesys`.)_

```
pintos -f -q
```

7. Run the tests.

```
cd ~/pintos/src/userprog/build
make check VERBOSE=1
```

8. To load and run the example user programs, you need to build them first.

```
cd ~/pintos/src/examples
make
cd ~/pintos/userprog/build
pintos -p ../../examples/echo -a echo -- -q
pintos -q run ’echo x’
```
