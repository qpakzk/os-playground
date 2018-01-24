### Installing _cmocka_ and running the C programming assignment

_host platform independent procedure_

_all versions as of 2018-01-23_

* * *

#### Prerequisites

1. An installation as in [virual-dev-env](https://github.com/ivogeorg/os-playground/blob/master/virtual-dev-env.md) or equivalent.

2. An installation as in [java-n-clion](https://github.com/ivogeorg/os-playground/edit/master/java-n-clion.md).


#### Installing the _cmocka_ unit testing framework for C

1. Download the generic Linux archive [cmocka-1.1.1.tar.xz](https://cmocka.org/files/1.1/cmocka-1.1.1.tar.xz).

2. Unpack and create a `build` directory.

  ```
  cd
  tar xvf ~/Downloads/cmocka-1.1.1.tar.xz
  cd cmocka-1.1.1
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
   /usr/local/include/cmocka_pbc.h
   /usr/local/include/cmocka.h
   /usr/local/lib/libcmocka.so.0
   /usr/local/lib/cmake/cmocka
   /usr/local/lib/cmake/cmocka/cmocka-config.cmake
   /usr/local/lib/cmake/cmocka/cmocka-config-version.cmake
   /usr/local/lib/libcmocka.so
   /usr/local/lib/libcmocka.so.0.4.1
   /usr/local/lib/pkgconfig/cmocka.pc
   ```

#### Running the test suite for the C programming assignment

1. Get a fresh fork of the [C Programming Assignment 3](https://github.com/ivogeorg/msl-clang-003) from Github.

2. Clone under `~/git-repos`.

3. Open CLion and open the `~/git-repos/msl-clang-003` project. The `CMakeLists.txt` has been modified to work with the installed `cmocka` library. You should be able to build the project and run the test suite.
