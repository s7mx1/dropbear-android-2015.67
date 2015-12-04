# dropbear-android-2015.67
dropbear-2015.67 for android. Reference: [here](http://forum.xda-developers.com/zenfone2/general/compiling-dropbear-2015-67-zenfone-2-t3142222) and [here](http://blog.xulforum.org/index.php?post/2013/12/19/Compiling-Dropbear-for-a-Nexus-7-tablet).

## How to compile
Install android-ndk-r10e and make standlone tool chains with the following command on your Ubuntu 14.04 64bit PC:
```
./make-standalone-toolchain.sh --arch=aarch64 --platform=android-21 --install-dir=/opt/android-toolchain-arm64 --ndk-dir=/opt/android-ndk-r10e --system=linux-x86_64

./make-standalone-toolchain.sh --arch=arm --platform=android-21 --install-dir=/opt/android-toolchain-arm --ndk-dir=/opt/android-ndk-r10e --system=linux-x86_64

./make-standalone-toolchain.sh --arch=x86_64 --platform=android-21 --install-dir=/opt/android-toolchain-x86_64 --ndk-dir=/opt/android-ndk-r10e --system=linux-x86_64
```
## Compile

Set path env
```
export PATH=/opt/android-toolchain-arm64/bin:/opt/android-toolchain-arm/bin:/opt/android-toolchain-x86_64/bin:$PATH
```

Set target for arm64, armhf or x86_64 system:
```
export HOST=aarch64-linux-android   # for arm64
export HOST=arm-linux-androideabi   # for armhf
export HOST=x86_64-linux-android   # for armhf
```
Configure
```
./configure --build=x86_64-unknown-linux-gnu --host=$HOST \
  --disable-zlib --disable-loginfunc \
  --disable-shadow --disable-utmp --disable-utmpx --disable-wtmp \
  --disable-wtmpx --disable-pututline --disable-pututxline --disable-lastlog
echo "#define USE_DEV_PTMX 1" >> config.h
```
Build
```
STATIC=1 MULTI=1 SCPPROGRESS=0 PROGRAMS="dropbear dropbearkey dropbearconvert scp dbclient" make strip
```
