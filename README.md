Simple edits and howto of the main xash3d-fwgs to be able to run on the RG350/RG350M

How to build :

Install the gcw0 toolchain in /opt/

git clone -- recursive https://github.com/citral23/xash3d-fwgs-mipsel.git

cd xash3d-fwgs-mipsel

export PATH="/opt/gcw0-toolchain/usr/bin/":$PATH
export CC="/opt/usr/bin/mipsel-gcw0-linux-uclibc-gcc"
export CXX="/opt/gcw0-toolchain//usr/bin/mipsel-gcw0-linux-uclibc-g++"
export FIND_ROOT_PATH=/opt/gcw0-toolchain/usr/
export CFLAGS="-fPIC"
export CXXFLAGS="-fPIC"

./waf configure -T release --enable-gles1 --enable-stbtt -s /opt/gcw0-toolchain/usr/mipsel-gcw0-linux-uclibc/sysroot/usr/
./waf build

git clone --recursive https://github.com/FWGS/hlsdk-xash3d.git
cd hlsdk-xash3d
./waf confire -T release
./waf build

Collect the generated .so in the build folders
