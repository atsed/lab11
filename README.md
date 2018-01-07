[![Build Status](https://travis-ci.org/desta-study/lab11.svg?branch=master)](https://travis-ci.org/desta-study/lab11)

## Laboratory work XI

Данная лабораторная работа посвещена изучению компонентов **Boost** на примере `program_options`

```ShellSession
$ open http://www.boost.org/doc/libs/1_65_0/doc/html/program_options.html
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab11** на сервисе **GitHub**
- [X] 2. Выполнить инструкцию учебного материала
- [X] 3. Ознакомиться со ссылками учебного материала
- [X] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Делаем первоначальные настройки, добавляя значения переменным окружения
```ShellSession
#Устанавливаем значение переменной окружения GITHUB_USERNAME
$ export GITHUB_USERNAME=desta-study
$ alias edit=vim
#Создаем алиас на команду sed
$ alias gsed=sed # for *-nix system
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/desta-study/workspace ~/desta-study/workspace
$ source scripts/activate
```

Проводим первоначальные настройки для соединения с репозиторием 11 лабораторной работы
```ShellSession
# Клонирование удаленного репозитория 10 лабораторной в локальный каталог 11 лабораторной
$ git clone https://github.com/${GITHUB_USERNAME}/lab10 lab11
Cloning into 'projects/lab11'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 14 (delta 1), reused 9 (delta 0), pack-reused 0
Unpacking objects: 100% (14/14), done.
Checking connectivity... done.
# Меняем директорию на lab11
$ cd lab11
# Отключаемся от удаленного репозитория 10 лабораторной
$ git remote remove origin
# Подключаемся к удаленному репозиторию 11 лабораторной
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab11
```
Подключаем пакеты boost::program_options через утилиту Hunter и редактируем demo.cpp и CMakeLists.txt
```ShellSession
# boost::program_options
#Редактируем CMakeLists.txt
$ edit CMakeLists.txt
#Редактируем sources/demo.cpp
$ edit sources/demo.cpp
```

Работа с CMake
```ShellSession
#-H. установка директория, в который сгенерируется файл CMakeLists.txt
#-B_build указывает директорию для собираемых файлов
#-D - заменяет команду set
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install # Сборка пакета с бинарным деревом проекта

-- The C compiler identification is GNU 5.4.0
-- The CXX compiler identification is GNU 5.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/desta-study/.hunter
-- [hunter] [ Hunter-ID: a7d8402 | Toolchain-ID: e1266bb | Config-ID: 83da1ac ]
-- [hunter] PRINT_ROOT: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Install (ver.: 0.1.0.0)
-- [hunter] BOOST_ROOT: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Install (ver.: 1.65.1)
-- [hunter] Building Boost
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/cache.cmake
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/args.cmake
-- The C compiler identification is GNU 5.4.0
-- The CXX compiler identification is GNU 5.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compile features
-- Detecting CXX compile features - done
CMake Warning (dev) at /usr/share/cmake-3.5/Modules/ExternalProject.cmake:1880 (if):
  Policy CMP0054 is not set: Only interpret if() arguments as variables or
  keywords when unquoted.  Run "cmake --help-policy CMP0054" for policy
  details.  Use the cmake_policy command to set the policy and suppress this
  warning.

  Quoted variables like "x" will no longer be dereferenced when the policy is
  set to NEW.  Since the policy is not set the OLD behavior will be used.
Call Stack (most recent call first):
  /usr/share/cmake-3.5/Modules/ExternalProject.cmake:2459 (_ep_add_download_command)
  CMakeLists.txt:90 (ExternalProject_Add)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done
-- Generating done
-- Build files have been written to: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/Build
Scanning dependencies of target Boost
[ 12%] Creating directories for 'Boost'
[ 25%] Performing download step (download, verify and extract) for 'Boost'
-- downloading...
     src='https://dl.bintray.com/boostorg/release/1.65.1/source/boost_1_65_1.tar.bz2'
     dst='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
     timeout='none'
-- [download 0% complete]
-- [download 1% complete]
-- [download 2% complete]
-- [download 3% complete]
-- [download 4% complete]
-- [download 5% complete]
-- [download 6% complete]
-- [download 7% complete]
-- [download 8% complete]
-- [download 9% complete]
-- [download 10% complete]
-- [download 11% complete]
-- [download 12% complete]
-- [download 13% complete]
-- [download 14% complete]
-- [download 15% complete]
-- [download 16% complete]
-- [download 17% complete]
-- [download 18% complete]
-- [download 19% complete]
-- [download 20% complete]
-- [download 21% complete]
-- [download 22% complete]
-- [download 23% complete]
-- [download 24% complete]
-- [download 25% complete]
-- [download 26% complete]
-- [download 27% complete]
-- [download 28% complete]
-- [download 29% complete]
-- [download 30% complete]
-- [download 31% complete]
-- [download 32% complete]
-- [download 33% complete]
-- [download 34% complete]
-- [download 35% complete]
-- [download 36% complete]
-- [download 37% complete]
-- [download 38% complete]
-- [download 39% complete]
-- [download 40% complete]
-- [download 41% complete]
-- [download 42% complete]
-- [download 43% complete]
-- [download 44% complete]
-- [download 45% complete]
-- [download 46% complete]
-- [download 47% complete]
-- [download 48% complete]
-- [download 49% complete]
-- [download 50% complete]
-- [download 51% complete]
-- [download 52% complete]
-- [download 53% complete]
-- [download 54% complete]
-- [download 55% complete]
-- [download 56% complete]
-- [download 57% complete]
-- [download 58% complete]
-- [download 59% complete]
-- [download 60% complete]
-- [download 61% complete]
-- [download 62% complete]
-- [download 63% complete]
-- [download 64% complete]
-- [download 65% complete]
-- [download 66% complete]
-- [download 67% complete]
-- [download 68% complete]
-- [download 69% complete]
-- [download 70% complete]
-- [download 71% complete]
-- [download 72% complete]
-- [download 73% complete]
-- [download 74% complete]
-- [download 75% complete]
-- [download 76% complete]
-- [download 77% complete]
-- [download 78% complete]
-- [download 79% complete]
-- [download 80% complete]
-- [download 81% complete]
-- [download 82% complete]
-- [download 83% complete]
-- [download 84% complete]
-- [download 85% complete]
-- [download 86% complete]
-- [download 87% complete]
-- [download 88% complete]
-- [download 89% complete]
-- [download 90% complete]
-- [download 91% complete]
-- [download 92% complete]
-- [download 93% complete]
-- [download 94% complete]
-- [download 95% complete]
-- [download 96% complete]
-- [download 97% complete]
-- [download 98% complete]
-- [download 99% complete]
-- [download 100% complete]
-- downloading... done
-- verifying file...
     file='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
-- verifying file... done
-- extracting...
     src='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
     dst='/home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 37%] No patch step for 'Boost'
[ 50%] No update step for 'Boost'
[ 62%] Performing configure step for 'Boost'
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Detecting Python version... 2.7
Detecting Python root... /usr
Unicode/ICU support for Boost.Regex?... not found.
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:

    ./b2
    
To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help
     
   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html
     
   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html

[ 75%] No build step for 'Boost'
[ 87%] Performing install step for 'Boost'
Performing configuration checks

    - 32-bit                   : no
    - 64-bit                   : yes
    - arm                      : no
    - mips1                    : no
    - power                    : no
    - sparc                    : no
    - x86                      : yes

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : not building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - metaparse                : not building
    - mpi                      : not building
    - program_options          : not building
    - python                   : not building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : not building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/args.cmake
[100%] Completed 'Boost'
[100%] Built target Boost
-- [hunter] Build step successful (dir: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost)
-- [hunter] Cache saved: /home/desta-study/.hunter/_Base/Cache/raw/7754257efee6e1387534eb5509fe6b5a5d5dcf5e.tar.bz2
-- [hunter] BOOST_ROOT: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Install (ver.: 1.65.1)
-- [hunter] Building Boost (component: system)
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/cache.cmake
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__system/args.cmake
-- The C compiler identification is GNU 5.4.0
-- The CXX compiler identification is GNU 5.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compile features
-- Detecting CXX compile features - done
CMake Warning (dev) at /usr/share/cmake-3.5/Modules/ExternalProject.cmake:1880 (if):
  Policy CMP0054 is not set: Only interpret if() arguments as variables or
  keywords when unquoted.  Run "cmake --help-policy CMP0054" for policy
  details.  Use the cmake_policy command to set the policy and suppress this
  warning.

  Quoted variables like "x" will no longer be dereferenced when the policy is
  set to NEW.  Since the policy is not set the OLD behavior will be used.
Call Stack (most recent call first):
  /usr/share/cmake-3.5/Modules/ExternalProject.cmake:2459 (_ep_add_download_command)
  CMakeLists.txt:345 (ExternalProject_Add)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done
-- Generating done
-- Build files have been written to: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__system/Build
Scanning dependencies of target Boost-system
[ 12%] Creating directories for 'Boost-system'
[ 25%] Performing download step (download, verify and extract) for 'Boost-system'
-- verifying file...
     file='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
-- verifying file... done
-- extracting...
     src='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
     dst='/home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__system/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 37%] No patch step for 'Boost-system'
[ 50%] No update step for 'Boost-system'
[ 62%] Performing configure step for 'Boost-system'
configure
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Detecting Python version... 2.7
Detecting Python root... /usr
Unicode/ICU support for Boost.Regex?... not found.
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:

    ./b2
    
To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help
     
   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html
     
   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html

[ 75%] Performing build step for 'Boost-system'
Performing configuration checks

    - 32-bit                   : no
    - 64-bit                   : yes
    - arm                      : no
    - mips1                    : no
    - power                    : no
    - sparc                    : no
    - x86                      : yes

Building the Boost C++ Libraries.


    - symlinks supported       : yes

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : not building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - metaparse                : not building
    - mpi                      : not building
    - program_options          : not building
    - python                   : not building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

...patience...
...found 174 targets...
...updating 20 targets...
common.mkdir bin.v2/libs
common.mkdir stage
common.mkdir bin.v2/libs/system
common.mkdir stage/lib
common.mkdir bin.v2/libs/system/build
common.mkdir bin.v2/libs/system/build/gcc-5.4.0
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/release
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/debug
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/release/link-static
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/debug/link-static
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/release/link-static/threading-multi
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/debug/link-static/threading-multi
gcc.compile.c++ bin.v2/libs/system/build/gcc-5.4.0/debug/link-static/threading-multi/error_code.o
gcc.archive bin.v2/libs/system/build/gcc-5.4.0/debug/link-static/threading-multi/libboost_system-mt-d.a
common.copy stage/lib/libboost_system-mt-d.a
gcc.compile.c++ bin.v2/libs/system/build/gcc-5.4.0/release/link-static/threading-multi/error_code.o
gcc.archive bin.v2/libs/system/build/gcc-5.4.0/release/link-static/threading-multi/libboost_system-mt.a
common.copy stage/lib/libboost_system-mt.a
...updated 20 targets...


The Boost C++ Libraries were successfully built!

The following directory should be added to compiler include paths:

    /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__system/Source

The following directory should be added to linker library paths:

    /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__system/Source/stage/lib

[ 87%] Performing install step for 'Boost-system'
Performing configuration checks

    - 32-bit                   : no  (cached)
    - 64-bit                   : yes (cached)
    - arm                      : no  (cached)
    - mips1                    : no  (cached)
    - power                    : no  (cached)
    - sparc                    : no  (cached)
    - x86                      : yes (cached)
    - symlinks supported       : yes (cached)

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : not building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - metaparse                : not building
    - mpi                      : not building
    - program_options          : not building
    - python                   : not building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

[100%] Completed 'Boost-system'
[100%] Built target Boost-system
-- [hunter] Build step successful (dir: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__system)
-- [hunter] Cache saved: /home/desta-study/.hunter/_Base/Cache/raw/9244173c2018496d3a0ed54b92d8cfd861d6c565.tar.bz2
-- [hunter] BOOST_ROOT: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Install (ver.: 1.65.1)
-- [hunter] Building Boost (component: filesystem)
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/cache.cmake
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__filesystem/args.cmake
-- The C compiler identification is GNU 5.4.0
-- The CXX compiler identification is GNU 5.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compile features
-- Detecting CXX compile features - done
CMake Warning (dev) at /usr/share/cmake-3.5/Modules/ExternalProject.cmake:1880 (if):
  Policy CMP0054 is not set: Only interpret if() arguments as variables or
  keywords when unquoted.  Run "cmake --help-policy CMP0054" for policy
  details.  Use the cmake_policy command to set the policy and suppress this
  warning.

  Quoted variables like "x" will no longer be dereferenced when the policy is
  set to NEW.  Since the policy is not set the OLD behavior will be used.
Call Stack (most recent call first):
  /usr/share/cmake-3.5/Modules/ExternalProject.cmake:2459 (_ep_add_download_command)
  CMakeLists.txt:345 (ExternalProject_Add)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done
-- Generating done
-- Build files have been written to: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__filesystem/Build
Scanning dependencies of target Boost-filesystem
[ 12%] Creating directories for 'Boost-filesystem'
[ 25%] Performing download step (download, verify and extract) for 'Boost-filesystem'
-- verifying file...
     file='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
-- verifying file... done
-- extracting...
     src='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
     dst='/home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__filesystem/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 37%] No patch step for 'Boost-filesystem'
[ 50%] No update step for 'Boost-filesystem'
[ 62%] Performing configure step for 'Boost-filesystem'
configure
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Detecting Python version... 2.7
Detecting Python root... /usr
Unicode/ICU support for Boost.Regex?... not found.
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:

    ./b2
    
To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help
     
   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html
     
   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html

[ 75%] Performing build step for 'Boost-filesystem'
Performing configuration checks

    - 32-bit                   : no
    - 64-bit                   : yes
    - arm                      : no
    - mips1                    : no
    - power                    : no
    - sparc                    : no
    - x86                      : yes

Building the Boost C++ Libraries.


    - symlinks supported       : yes

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - metaparse                : not building
    - mpi                      : not building
    - program_options          : not building
    - python                   : not building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : not building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

...patience...
...found 704 targets...
...updating 51 targets...
common.mkdir stage
common.mkdir bin.v2/libs
common.mkdir stage/lib
common.mkdir bin.v2/libs/system
common.mkdir bin.v2/libs/filesystem
common.mkdir bin.v2/libs/system/build
common.mkdir bin.v2/libs/filesystem/build
common.mkdir bin.v2/libs/system/build/gcc-5.4.0
common.mkdir bin.v2/libs/filesystem/build/gcc-5.4.0
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/release
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/debug
common.mkdir bin.v2/libs/filesystem/build/gcc-5.4.0/release
common.mkdir bin.v2/libs/filesystem/build/gcc-5.4.0/debug
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/release/link-static
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/debug/link-static
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/release/link-static/threading-multi
common.mkdir bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static
common.mkdir bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static
common.mkdir bin.v2/libs/system/build/gcc-5.4.0/debug/link-static/threading-multi
common.mkdir bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi
common.mkdir bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi
gcc.compile.c++ bin.v2/libs/system/build/gcc-5.4.0/debug/link-static/threading-multi/error_code.o
gcc.archive bin.v2/libs/system/build/gcc-5.4.0/debug/link-static/threading-multi/libboost_system-mt-d.a
common.copy stage/lib/libboost_system-mt-d.a
gcc.compile.c++ bin.v2/libs/system/build/gcc-5.4.0/release/link-static/threading-multi/error_code.o
gcc.archive bin.v2/libs/system/build/gcc-5.4.0/release/link-static/threading-multi/libboost_system-mt.a
common.copy stage/lib/libboost_system-mt.a
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/path_traits.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/codecvt_error_category.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/codecvt_error_category.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/portability.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/path_traits.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/windows_file_codecvt.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/path.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/portability.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/utf8_codecvt_facet.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/unique_path.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/windows_file_codecvt.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/operations.o
gcc.archive bin.v2/libs/filesystem/build/gcc-5.4.0/debug/link-static/threading-multi/libboost_filesystem-mt-d.a
common.copy stage/lib/libboost_filesystem-mt-d.a
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/utf8_codecvt_facet.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/unique_path.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/path.o
gcc.compile.c++ bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/operations.o
gcc.archive bin.v2/libs/filesystem/build/gcc-5.4.0/release/link-static/threading-multi/libboost_filesystem-mt.a
common.copy stage/lib/libboost_filesystem-mt.a
...updated 51 targets...


The Boost C++ Libraries were successfully built!

The following directory should be added to compiler include paths:

    /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__filesystem/Source

The following directory should be added to linker library paths:

    /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__filesystem/Source/stage/lib

[ 87%] Performing install step for 'Boost-filesystem'
Performing configuration checks

    - 32-bit                   : no  (cached)
    - 64-bit                   : yes (cached)
    - arm                      : no  (cached)
    - mips1                    : no  (cached)
    - power                    : no  (cached)
    - sparc                    : no  (cached)
    - x86                      : yes (cached)
    - symlinks supported       : yes (cached)

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - metaparse                : not building
    - mpi                      : not building
    - program_options          : not building
    - python                   : not building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : not building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

[100%] Completed 'Boost-filesystem'
[100%] Built target Boost-filesystem
-- [hunter] Build step successful (dir: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__filesystem)
-- [hunter] Cache saved: /home/desta-study/.hunter/_Base/Cache/raw/4eae42d4535ba71ab91bada197dab3bf423174e2.tar.bz2
-- [hunter] BOOST_ROOT: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Install (ver.: 1.65.1)
-- [hunter] Building Boost (component: program_options)
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/cache.cmake
loading initial cache file /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__program_options/args.cmake
-- The C compiler identification is GNU 5.4.0
-- The CXX compiler identification is GNU 5.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compile features
-- Detecting CXX compile features - done
CMake Warning (dev) at /usr/share/cmake-3.5/Modules/ExternalProject.cmake:1880 (if):
  Policy CMP0054 is not set: Only interpret if() arguments as variables or
  keywords when unquoted.  Run "cmake --help-policy CMP0054" for policy
  details.  Use the cmake_policy command to set the policy and suppress this
  warning.

  Quoted variables like "x" will no longer be dereferenced when the policy is
  set to NEW.  Since the policy is not set the OLD behavior will be used.
Call Stack (most recent call first):
  /usr/share/cmake-3.5/Modules/ExternalProject.cmake:2459 (_ep_add_download_command)
  CMakeLists.txt:345 (ExternalProject_Add)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done
-- Generating done
-- Build files have been written to: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__program_options/Build
Scanning dependencies of target Boost-program_options
[ 12%] Creating directories for 'Boost-program_options'
[ 25%] Performing download step (download, verify and extract) for 'Boost-program_options'
-- verifying file...
     file='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
-- verifying file... done
-- extracting...
     src='/home/desta-study/.hunter/_Base/Download/Boost/1.65.1/4a5b0c3/boost_1_65_1.tar.bz2'
     dst='/home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__program_options/Source'
-- extracting... [tar xfz]
-- extracting... [analysis]
-- extracting... [rename]
-- extracting... [clean up]
-- extracting... done
[ 37%] No patch step for 'Boost-program_options'
[ 50%] No update step for 'Boost-program_options'
[ 62%] Performing configure step for 'Boost-program_options'
configure
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Detecting Python version... 2.7
Detecting Python root... /usr
Unicode/ICU support for Boost.Regex?... not found.
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:

    ./b2
    
To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help
     
   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html
     
   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html

[ 75%] Performing build step for 'Boost-program_options'
Performing configuration checks

    - 32-bit                   : no
    - 64-bit                   : yes
    - arm                      : no
    - mips1                    : no
    - power                    : no
    - sparc                    : no
    - x86                      : yes

Building the Boost C++ Libraries.


    - symlinks supported       : yes

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : not building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - metaparse                : not building
    - mpi                      : not building
    - program_options          : building
    - python                   : not building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : not building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

...patience...
...found 1021 targets...
...updating 40 targets...
common.mkdir stage
common.mkdir bin.v2/libs
common.mkdir stage/lib
common.mkdir bin.v2/libs/program_options
common.mkdir bin.v2/libs/program_options/build
common.mkdir bin.v2/libs/program_options/build/gcc-5.4.0
common.mkdir bin.v2/libs/program_options/build/gcc-5.4.0/debug
common.mkdir bin.v2/libs/program_options/build/gcc-5.4.0/release
common.mkdir bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static
common.mkdir bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static
common.mkdir bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi
common.mkdir bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/positional_options.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/config_file.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/config_file.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/parsers.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/value_semantic.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/variables_map.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/options_description.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/cmdline.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/utf8_codecvt_facet.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/positional_options.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/convert.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/utf8_codecvt_facet.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/cmdline.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/winmain.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/convert.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/variables_map.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/split.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/options_description.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/winmain.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/parsers.o
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/value_semantic.o
gcc.archive bin.v2/libs/program_options/build/gcc-5.4.0/release/link-static/threading-multi/libboost_program_options-mt.a
common.copy stage/lib/libboost_program_options-mt.a
gcc.compile.c++ bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/split.o
gcc.archive bin.v2/libs/program_options/build/gcc-5.4.0/debug/link-static/threading-multi/libboost_program_options-mt-d.a
common.copy stage/lib/libboost_program_options-mt-d.a
...updated 40 targets...


The Boost C++ Libraries were successfully built!

The following directory should be added to compiler include paths:

    /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__program_options/Source

The following directory should be added to linker library paths:

    /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__program_options/Source/stage/lib

[ 87%] Performing install step for 'Boost-program_options'
Performing configuration checks

    - 32-bit                   : no  (cached)
    - 64-bit                   : yes (cached)
    - arm                      : no  (cached)
    - mips1                    : no  (cached)
    - power                    : no  (cached)
    - sparc                    : no  (cached)
    - x86                      : yes (cached)
    - symlinks supported       : yes (cached)

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : not building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - metaparse                : not building
    - mpi                      : not building
    - program_options          : building
    - python                   : not building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : not building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

[100%] Completed 'Boost-program_options'
[100%] Built target Boost-program_options
-- [hunter] Build step successful (dir: /home/desta-study/.hunter/_Base/a7d8402/e1266bb/83da1ac/Build/Boost/__program_options)
-- [hunter] Cache saved: /home/desta-study/.hunter/_Base/Cache/raw/78cd2c44479dd76445358744cc646118d6cfb001.tar.bz2
-- Boost version: 1.65.1
-- Found the following Boost libraries:
--   system
--   filesystem
--   program_options
-- Configuring done
-- Generating done
-- Build files have been written to: /home/desta-study/desta-study/workspace/projects/lab11/_build

$ cmake --build _build --target install

Scanning dependencies of target demo
[ 50%] Building CXX object CMakeFiles/demo.dir/sources/demo.cpp.o
[100%] Linking CXX executable demo
[100%] Built target demo
Install the project...
-- Install configuration: ""
-- Installing: /home/desta-study/desta-study/workspace/projects/lab11/_install/bin/demo

$ mkdir artifacts && cd artifacts # Создаем директорию artifacts и переходим в неё
```
Создаем default.log
```ShellSession
# C помощью нашей программы записываем "text1 text2 text3" в default.log
$ echo "text1 text2 text3" | ../_install/bin/demo
DEFAULT
# Проверяем наличие данного файла
$ test -f default.log
# Если 0, то файл существует
$ echo $?
0
```
Создаем config.log
```ShellSession
# Создаем директорию ${HOME}/.config
$ mkdir ${HOME}/.config
# Вводим в demo.cfg значение output=config.log 
$ echo "output=config.log" > ${HOME}/.config/demo.cfg
# C помощью нашей программы записываем "text1 text2 text3" в config.log
$ echo "text1 text2 text3" | ../_install/bin/demo
# Проверяем наличие данного файла
$ test -f config.log
# Если 0, то файл существует
$ echo $?
0
```
Создаем env.log
```ShellSession
# Экспортируем глобальную переменную окружения DEMO_OUTPUT
$ export DEMO_OUTPUT=env.log
# C помощью нашей программы записываем "text1 text2 text3" в env.log
$ echo "text1 text2 text3" | ../_install/bin/demo
# Проверяем наличие данного файла
$ test -f env.log
# Если 0, то файл существует
$ echo $?
0
```
Создаем arg.log
```ShellSession
# C помощью нашей программы записываем "text1 text2 text3" в arg.log, задавая его с помощью --output
$ echo "text1 text2 text3" | ../_install/bin/demo --output arg.log
# Проверяем наличие данного файла
$ test -f arg.log
# Если 0, то файл существует
$ echo $?
0
```
Редактируем .travis.yml
```ShellSession
$ cat >> .travis.yml <<EOF
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build --target install
- mkdir artifacts && cd artifacts
- echo "text1 text2 text3" | ../_install/bin/demo
- test -f default.log
- mkdir ${HOME}/.config
- echo "output=config.log" > ${HOME}/.config/demo.cfg
- echo "text1 text2 text3" | ../_install/bin/demo
- test -f config.log
- export DEMO_OUTPUT=env.log
- echo "text1 text2 text3" | ../_install/bin/demo
- test -f env.log
- echo "text1 text2 text3" | ../_install/bin/demo --output arg.log
- test -f arg.log
EOF
```
Редактируем README.md
```ShellSession
# Редактируем README.md
gsed -i 's/lab10/lab11/g' README.md
```
Отправляем последние изменения на GitHub сервер
```ShellSession
# Добавляем все отредактированные файлы в подтвержденные
$ git add .
# Коммитим наш репозиторий с сообщением
$ git commit -m"changed format output"

[master 104b3b9] changed format output
 7 files changed, 112 insertions(+), 12 deletions(-)
 create mode 100644 artifacts/.travis.yml
 create mode 100644 artifacts/config.log
 create mode 100644 artifacts/default.log
 create mode 100644 artifacts/env.log
 rewrite sources/demo.cpp (87%)

# Выгружаем наш локальный репозиторий в удалённый
$ git push origin master

Username for 'https://github.com': desta-study
Password for 'https://desta-study@github.com': 
Counting objects: 23, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (23/23), 7.88 KiB | 0 bytes/s, done.
Total 23 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), done.
To https://github.com/desta-study/lab11
 * [new branch]      master -> master
```
Работа с Travis
```ShellSession
# Авторизуемся своим GITHUB аккаунтом
$ travis login --auto
We need your GitHub login to identify you.
This information will not be sent to Travis CI, only to api.github.com.
The password will not be displayed.

Try running with --github-token or --auto if you don't want to enter your password anyway.

Username: desta-study
Password for desta-study: *************
Successfully logged in as desta-study!
# Включаем репозиторий в Travis
$ travis enable
Detected repository as desta-study/lab11, is this correct? |yes| yes
desta-study/lab11: enabled :)
```

## Report

```ShellSession
$ popd
$ export LAB_NUMBER=11
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [String Algorithms](http://www.boost.org/doc/libs/1_65_0/doc/html/string_algo.html)
- [Date Time](http://www.boost.org/doc/libs/1_65_0/doc/html/date_time.html)
- [DLL](http://www.boost.org/doc/libs/1_65_0/doc/html/boost_dll.html)
- [Heap](http://www.boost.org/doc/libs/1_65_0/doc/html/heap.html)
- [Interprocess](http://www.boost.org/doc/libs/1_65_0/doc/html/interprocess.html)
- [Lockfree](http://www.boost.org/doc/libs/1_65_0/doc/html/lockfree.html)
- [Lexicalcast](http://www.boost.org/doc/libs/1_65_0/doc/html/boost_lexical_cast.html)
- [Property Tree](http://www.boost.org/doc/libs/1_65_0/doc/html/property_tree.html)

```
Copyright (c) 2017 Братья Вершинины
```
