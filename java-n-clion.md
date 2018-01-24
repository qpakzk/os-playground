### Installing Java and CLion

_host platform independent procedure_

_all versions as of 2018-01-23_

* * *

#### Prerequisites

1. An installation as in [virual-dev-env](https://github.com/ivogeorg/os-playground/blob/master/virtual-dev-env.md) or equivalent.

#### Install Java

The [CLion IDE](https://www.jetbrains.com/clion/) requires a JVM to run. The follwoing installs Java 8. Not the latest, but enough for CLion.

```
sudo apt-get update
java -version
sudo apt-get install default-jre
java -version
sudo apt-get install default-jdk
```

#### Update gcc/g++

The default `gcc` version installed on the Ubuntu desktop (16.04.3 LTS) is 5.4. If you want to update to the latest and/or have version alternatives, follow the instructions [here](https://gist.github.com/application2000/73fd6f4bf1be6600a2cf9f56315a2d91).

#### Install CLion

1. Download the Linux archive from the [website](https://www.jetbrains.com/clion/download/#section=linux-version).

2. Check the SHA sum and compare againt the value provided by the download page:

   ```
   sha256sum ~/Downloads/CLion-2017.3.2.tar.gz
   ```

3. Unpack.

   ```
   cd
   tar xfz ~/Downloads/CLion-2017.3.2.tar.gz
   ```

4. Add the `~/clion-1.2.4/bin` directory to your `$PATH` variable.

  1. Open an editor.
  
     ```
     gedit ~/.bashrc
     ```
  
  2. Add the following line to the end of the file.
  
     ```
     export PATH=$HOME/clion-2017.3.2/bin:$PATH
     ```
  
  3. Run from anywhere.
  
     ```
     clion.sh
     ```
  
  4. When CLion opens, enter your account and/or license, and proceed with all the defaults. There are some optional tools you can install/enable.
  
  5. When CLion opens, its icon will appear in the left-hand bar. You can right-click and select "Lock to Launcher". The current version actually asks you if you want to create a menu icon.
  
  6. If you have installed the optional tools, it is likely that CLion will default to a _Vim emulation mode_. `vi`/`vim` is one of the most popular editors with Linux geeks. Unless you have experience with it, it can be confusing. You can turn it off by going to **Tools-->Vim Emulator**.
  
  7. Note that the keymap might be very different from what you are used to. To change the keymap, go to **File-->Settings...** and select **Keymap**.
  
