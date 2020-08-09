Simple edits of the main xash3d-fwgs to be able to compile for the RG350M (should also work on the RG350)

How to build :

Install the gcw0 toolchain in /opt/

git clone --branch mipsel --recursive https://github.com/citral23/xash3d-fwgs-mipsel.git

cd xash3d-fwgs-mipsel

export PATH="/opt/gcw0-toolchain/usr/bin/":$PATH

export CC="/opt/gcw0-toolchain/usr/bin/mipsel-gcw0-linux-uclibc-gcc"

export CXX="/opt/gcw0-toolchain/usr/bin/mipsel-gcw0-linux-uclibc-g++"

export FIND_ROOT_PATH=/opt/gcw0-toolchain/usr/

export CFLAGS="-fPIC"

export CXXFLAGS="-fPIC"

./waf configure -T release --enable-gles1 --enable-stbtt -s /opt/gcw0-toolchain/usr/mipsel-gcw0-linux-uclibc/sysroot/usr/

./waf build


cd hlsdk-xash3d

./waf configure -T release

./waf build

Collect the generated .so in the build folders and the xash3d binary, copy them all on your RG350M to a folder, and also copy your valve folder in that folder

Edit valve/gameinfo.txt and replace hl.dll with hl.so (You may also have to rename the libref_glxx library you want to use to libref_gl.so for xash3d to find it)

List of files/folder needed :
client_mipsel.so
hl_mipsel.so
libmenu.so
libref_gl.so
libxash.so
valve/
xash3d

Create a launch script in your xash3d folder :


#!/bin/sh

export XASH3D_BASEDIR=/your/path/Xash3D

export LD_LIBRARY_PATH=.

./xash3d


run that script and enjoy halflife at 20-60fps

If something goes wrong, edit the script to run "./xash3d -dev 5"

TODO : 

- work on controls
- configure the crash handler ucontext for mips
- rebuild once the new cl20 kernel/toolchain are out (gles2 might work with the updated etnaviv driver)


