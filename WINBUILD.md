mkdir dev
cd dev

mkdir lcsshare-build
cd lcsshare-build

zypper install git
git clone git://github.com/abzahri/owncloud-mirall.git ../lcsshare

zypper ar http://download.opensuse.org/repositories/windows:/mingw:/win32/openSUSE_12.1/windows:mingw:win32.repo
zypper ar http://download.opensuse.org/repositories/windows:/mingw/openSUSE_12.1/windows:mingw.repo
zypper ar http://pmbs.links2linux.org/download/mingw/32/openSUSE_12.1/ 'Custom NSIS'

zypper install cmake make mingw32-cross-binutils mingw32-cross-cpp mingw32-cross-gcc \
mingw32-cross-gcc-c++ mingw32-cross-pkg-config mingw32-filesystem mingw32-headers \
mingw32-runtime site-config mingw32-libqt5-sql mingw32-libqt5-sql-sqlite mingw32-sqlite \
mingw32-sqlite-devel mingw32-libssh2-devel kdewin-png2ico mingw32-libqt5 \
mingw32-libqt5-devel mingw32-libgcrypt mingw32-libgnutls mingw32-libneon-openssl \
mingw32-libneon-devel mingw32-libbeecrypt mingw32-libopenssl mingw32-openssl \
mingw32-libpng-devel mingw32-libsqlite3-0 mingw32-qt5keychain mingw32-qt5keychain-devel \
mingw32-libintl-devel mingw32-libneon-devel mingw32-libopenssl-devel mingw32-libproxy-devel \
mingw32-libxml2-devel mingw32-zlib-devel mingw32-qt5keychain-devel \
mingw32-libqt5-qtbase mingw32-libqt5-qtwinextras-devel mingw32-libqt5-qtserialport-devel \
mingw32-libqt5-qtquickcontrols mingw32-libqt5-qtimageformats-devel \
mingw32-libqt5-qtdeclarative mingw32-libqt5-qtactiveqt mingw32-cross-libqt5-qttools \
mingw32-libqt5-qtsensors mingw32-libqt5-qtwinextras mingw32-libqt5-qtxmlpatterns-devel \
mingw32-libqt5-qmldevtools-devel mingw32-libqt5-qtbase-devel mingw32-libqt5-qtmultimedia \
mingw32-libqt5-qtsvg-devel mingw32-libqt5-qtmultimedia-devel mingw32-cross-libqt5-qmake \
mingw32-libqt5-qtscript mingw32-libqt5-qtwebkit mingw32-libqt5-qttools \
mingw32-qt5keychain mingw32-libqt5-qttranslations mingw32-libqt5-qmldevtools \
mingw32-libqt5-qtserialport mingw32-libqt5-qtsensors-devel mingw32-libqt5-qtimageformats \
mingw32-libqt5-qtsvg mingw32-libqt5-qtxmlpatterns mingw32-angleproject-devel libneon-devel

zypper install mingw32-cross-nsis vi 
rpm -ihv http://download.tomahawk-player.org/packman/mingw:32/openSUSE_12.1/i586/mingw32-cross-nsis-plugin-processes-0-1.1.i586.rpm
rpm -ihv http://download.tomahawk-player.org/packman/mingw:32/openSUSE_12.1/i586/mingw32-cross-nsis-plugin-uac-0-3.1.i586.rpm
wget ftp://85.130.111.122/Install/last_ipgets/server_bc/libwinpthread-1.dll /usr/i686-w64-mingw32/sys-root/i686-w64-mingw32/bin/libwinpthread-1.dll

cmake -DCMAKE_BUILD_TYPE="Debug" ../lcsshare -DCMAKE_TOOLCHAIN_FILE=../lcsshare/admin/win/Toolchain-mingw32-openSUSE.cmake -Wno-dev

make package
