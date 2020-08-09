Simple edits and howto of the main xash3d-fwgs to be able to run on the RG350/RG350M

How to build :

Install the gcw0 toolchain in /opt/

git clone -- recursive https://github.com/citral23/xash3d-fwgs-mipsel.git

cd xash3d-fwgs-mipsel

cd ref_gl

git clone --recursive https://github.com/FWGS/nanogl.git

git clone --recursive https://github.com/FWGS/gl4es.git

cd ..

export PATH="/opt/gcw0-toolchain/usr/bin/":$PATH

export CC="/opt/usr/bin/mipsel-gcw0-linux-uclibc-gcc"

export CXX="/opt/gcw0-toolchain//usr/bin/mipsel-gcw0-linux-uclibc-g++"

export FIND_ROOT_PATH=/opt/gcw0-toolchain/usr/

export CFLAGS="-fPIC"

export CXXFLAGS="-fPIC"

./waf configure -T release --enable-gles1 --enable-stbtt -s /opt/gcw0-toolchain/usr/mipsel-gcw0-linux-uclibc/sysroot/usr/

(or as an alternative, --enable-gl4es which will compile an opengl to gles2 driver, looks a bit better in game but seems slower)

./waf build


cd hlsdk-xash3d

./waf confire -T release

./waf build

Collect the generated .so in the build folders and the xash3d binary, copy them all on your RG350 to a folder, and also copy your valve folder in that folder
Edit valve/gameinfo.txt and replace hl.dll with hl.so

Create a launch script in your xash3d folder :

#!/bin/sh
export XASH3D_BASEDIR=/your/path/Xash3D
export LD_LIBRARY_PATH=.
./xash3d

run that script and enjoy halflife at 20-60fps



