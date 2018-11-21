# Cross-Compiling Pyrite QT for Windows 

This document explains how to build Windows binaries from a Linux
system. We use MXE to cross-compile.

# Starting system

Have a Debian or Debian-derived system, like Ubuntu or Mint Linux.

# Building from source using mnt folder in Linux

# Install MXE requirements

http://mxe.cc/#requirements-debian

     $ cd mnt
    
install cross compile environment
Install mxe dependencies:
  ```$  apt-get install p7zip-full autoconf automake autopoint bash bison bzip2 cmake flex gettext git g++ gperf intltool libffi-dev libtool libltdl-dev libssl-dev libxml-parser-perl make openssl patch perl pkg-config python ruby scons sed unzip wget xz-utils libtool-bin libgtk2.0-dev```
  
  For 64-bit Ubuntu also install:
  
  ``` $  apt-get install g++-multilib libc6-dev-i386```
  
Clone mxe github repo
  ``` $  git clone https://github.com/mxe/mxe.git```

Build MXE
Add `MXE_TARGETS` so that we get 32-bit Windows binaries.

```
$ make MXE_TARGETS='i686-w64-mingw32.static' cc
$ make MXE_TARGETS='i686-w64-mingw32.static' qt
$ make MXE_TARGETS='i686-w64-mingw32.static' qttools
$ make MXE_TARGETS="i686-w64-mingw32.static" boost
```
Build OpenSSL for windows (version 1.1.x doesn't work)
```
    $ wget https://www.openssl.org/source/openssl-1.0.2d.tar.gz
    $ tar -xzvf openssl-1.0.2d.tar.gz
    $ cp -R openssl-1.0.2d openssl-win32-build
    $ cd openssl-win32-build
    $ CROSS_COMPILE="i686-w64-mingw32.static-" ./Configure mingw no-asm no-shared --prefix=/mnt/mxe/usr/i686-w64-mingw32.static
    $ make
    $  make install
    $ cd ..
 ```
    
Compiling berkley db:
Download and unpack berkeley db:
```
    $ cd /mnt
    $ wget http://download.oracle.com/berkeley-db/db-6.2.32.tar.gz
    $ tar zxvf db-6.2.32.tar.gz
```
Make bash script for compilation:
```
    $ cd /mnt/db-6.2.32
    $ touch compile-db.sh
    $ chmod ugo+x compile-db.sh
```
Content of compile-db.sh:
   ` $ nano compile-db.sh `
```
///////////////////////////////////////////////////////
#!/bin/bash
MXE_PATH=/mnt/mxe
sed -i "s/WinIoCtl.h/winioctl.h/g" src/dbinc/win_db.h
mkdir build_mxe
cd build_mxe

CC=$MXE_PATH/usr/bin/i686-w64-mingw32.static-gcc \
CXX=$MXE_PATH/usr/bin/i686-w64-mingw32.static-g++ \
../dist/configure \
	--disable-replication \
	--enable-mingw \
	--enable-cxx \
	--host x86 \
	--prefix=$MXE_PATH/usr/i686-w64-mingw32.static
make
make install
///////////////////////////////////////////////////////
```

Compile:
    `$ ./compile-db.sh`

Compiling miniupnpc:
Download and unpack miniupnpc:
```
    $ cd /mnt
    $ wget http://miniupnp.free.fr/files/miniupnpc-1.9.tar.gz
    $ tar zxvf miniupnpc-1.9.tar.gz
```
Make bash script for compilation:
```
    $ cd /mnt/miniupnpc-1.9
    $ touch compile-m.sh
    $ chmod ugo+x compile-m.sh
```
Content of compile-m.sh:
```
///////////////////////////////////////////////////////////////////////////
#!/bin/bash
MXE_PATH=/mnt/mxe
CC=$MXE_PATH/usr/bin/i686-w64-mingw32.static-gcc \
AR=$MXE_PATH/usr/bin/i686-w64-mingw32.static-ar \
CFLAGS="-DSTATICLIB -I$MXE_PATH/usr/i686-w64-mingw32.static/include" \
LDFLAGS="-L$MXE_PATH/usr/i686-w64-mingw32.static/lib" \
make libminiupnpc.a
mkdir $MXE_PATH/usr/i686-w64-mingw32.static/include/miniupnpc
cp *.h $MXE_PATH/usr/i686-w64-mingw32.static/include/miniupnpc
cp libminiupnpc.a $MXE_PATH/usr/i686-w64-mingw32.static/lib
////////////////////////////////////////////////////////////////////////////
```
Compile:
```
    $ ./compile-m.sh
    $ cd ..
```

Build qrencode QR
Clone mSIGNA repository, in case you haven't done so already:
```
    $ cd mnt
    $ git clone https://github.com/ciphrex/mSIGNA.git
```
Build qrencode QR Code C library (libqrencode) for Windows
```
    $ cd mSIGNA/deps/qrencode-3.4.3
    $ ./configure --host=i686-w64-mingw32.static --prefix=/mnt/mxe/usr/i686-w64-mingw32.static --without-tools --enable-static --disable-shared
    $ make
    $  make install
    $ cd ../../..
```
    
# Build Windows executables

Add the path to MXE plus `usr/bin` to your `PATH`:
```
    $ export PATH=/mnt/mxe/usr/bin:$PATH
```
To make a Windows executable, clone the Pyrite repository to /mnt/  folder 
 ```
    $ cd /mnt
    $ git clone https://github.com/pyritepirate/pyrite.git
```
Make bash script for compilation:
```
    $ cd /mnt/pyrite
    $ touch compile-pyrite.sh
    $ chmod ugo+x compile-pyrite.sh
```
Content of compile-pyrite.sh:
   ```  $ nano compile-pyrite.sh```
   ```
//////////////////////////////////////////////////////////////////////////////////////////////
#!/bin/bash
MXE_INCLUDE_PATH=/mnt/mxe/usr/i686-w64-mingw32.static/include
MXE_LIB_PATH=/mnt/mxe/usr/i686-w64-mingw32.static/lib
i686-w64-mingw32.static-qmake-qt5 \
	BOOST_LIB_SUFFIX=-mt \
	BOOST_THREAD_LIB_SUFFIX=_win32-mt \
	BOOST_INCLUDE_PATH=$MXE_INCLUDE_PATH/boost \
	BOOST_LIB_PATH=$MXE_LIB_PATH \
	OPENSSL_INCLUDE_PATH=$MXE_INCLUDE_PATH/openssl \
	OPENSSL_LIB_PATH=$MXE_LIB_PATH \
	BDB_INCLUDE_PATH=$MXE_INCLUDE_PATH \
	BDB_LIB_PATH=$MXE_LIB_PATH \
	MINIUPNPC_INCLUDE_PATH=$MXE_INCLUDE_PATH \
	MINIUPNPC_LIB_PATH=$MXE_LIB_PATH \
	QRENCODE_INCLUDE_PATH=$MXE_INCLUDE_PATH \
        QRENCODE_LIB_PATH=$MXE_LIB_PATH \
	QMAKE_LRELEASE=/mnt/mxe/usr/i686-w64-mingw32.static/qt5/bin/lrelease pyrite-qt.pro
make -f Makefile.Release
////////////////////////////////////////////////////////////////////////////////////////////////
```

to avoid /build_detect_platform: Permission denied error , do :
`chmod 755 src/leveldb/build_detect_platform`


compile Pyrite
     ``` $ ./compile-pyrite.sh```
      

output :``` $ ./compile-pyrite.sh ``` will create a file called `release/pyrite-qt.exe`
