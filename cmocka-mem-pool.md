### Installing _cmocka_ and running the C programming assigment

_host platform independent procedure_

_all versions as of 2016-03-09_

* * *

#### Prerequisites

1. An installation as in [virual-dev-env](https://github.com/ivogeorg/os-playground/blob/master/virtual-dev-env.md) or equivalent.

2. An installation as in [java-n-clion](https://github.com/ivogeorg/os-playground/edit/master/java-n-clion.md).


#### Installing the _cmocka_ unit testing framework for C

1. Download the generic Linux archive [cmocka-1.0.1.tar.xz](https://cmocka.org/files/1.0/cmocka-1.0.1.tar.xz).

2. Unpack and create a `build` directory.

  ```
  cd
  tar xvf ~/Downloads/cmocka-1.0.1.tar.xz
  cd cmocka-1.0.1
  mkdir build
  cd build
  ```

3. Build and install the `cmocka` library.

  ```
  cmake ..
  make
  sudo make install
  ```
  
4. On Ubuntu, this will install the library in the default location `/usr/local/lib`.

   ```
   find / -name "*cmocka*"
   ```
   
   will output, among other things,
   
   ```
   /usr/local/include/cmocka.h
   /usr/local/include/cmocka_pbc.h
   /usr/local/lib/libcmocka.so
   /usr/local/lib/libcmocka.so.0
   /usr/local/lib/libcmocka.so.0.3.1
   /usr/local/lib/pkgconfig/cmocka.pc
   /usr/local/lib/cmake/cmocka
   /usr/local/lib/cmake/cmocka/cmocka-config.cmake
   /usr/local/lib/cmake/cmocka/cmocka-config-version.cmake
   ```

#### Running the test suite for the C programming assignment

1. Get a fresh fork of the C programming assignment [Github repository](https://github.com/ivogeorg/denver-os-pa-c).

2. Clone under `~/git-repos`.

3. Open CLion and open the `~/git-repos/denver-os-pa-c` project. The `CMakeLists.txt` has been modified to work with the installed `cmocka` library. You should be able to build the project and run the test suite.
