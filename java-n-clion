### Installing Java and CLion

_host platform independent procedure_

_all versions as of 2016-03-09_

* * *

#### Install Java

The [CLion IDE](https://www.jetbrains.com/clion/) requires a JVM to run. The follwoing installs Java 7. Not the latest, but enough for CLion.

```
sudo apt-get update
java -version
sudo apt-get install default-jre
java -version
sudo apt-get install default-jdk
```

#### Update gcc/g++

The default `gcc` version installed on the Ubuntu desktop (14.04.4 LTS) is 4.8. The following will upgrade it to 4.9, which has full support for C++11.

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install gcc-4.9 g++-4.9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 60 --slave /usr/bin/g++ g++ /usr/bin/g++-4.9
```

#### Install CLion

1. Download the Linux archive from the [website](https://www.jetbrains.com/clion/download/#section=linux-version).

2. Check the SHA sum and compare againt the value provided by the download page:

```
sha256sum ~/Downloads/clion-1.2.4.tar.gz
```

3. Unpack.

```
cd
tar xfz ~/Downloads/clion-1.2.4.tar.gz
```

4. Add the `~/clion-1.2.4/bin` directory to your `$PATH` variable.

  1. Open an editor.
  
  ```
  gedit ~/.bashrc
  ```
  
  2. Add the following line to the end of the file.
  
  ```
  export PATH=$HOME/clion-1.2.4/bin:$PATH
  ```
  
  3. Run from anywhere.
  
  ```
  clion.sh
  ```
  
  4. When CLion opens, enter your account and/or license, and proceed with all the defaults. There are some optional tools you can install/enable.
  
  5. When CLion opens, its icon will appear in the left-hand bar. You can right-click and select "Lock to Launcher".
  
  6. If you have installed the optional tools, it is likely that CLion will default to a _Vim emulation mode_. `vi`/`vim` is one of the most popular editors with Linux geeks. Unless you have experience with it, it can be confusing. You can turn it off by going to **Tools-->Vim Emulator**.
  
  7. Note that the keymap might be very different from what you are used to. To change the keymap, go to **File-->Settings...** and select **Keymap**.
  
