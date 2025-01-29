### 在Linux上編譯
```bash
mkdir build
cd build
cmake ..
make -j4
make install
```

在conda中安裝
失敗不可行。
```bash
rm -rf build
mkdir build
cd build

cmake .. \
  -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_C_COMPILER=gcc \
  -DCMAKE_CXX_COMPILER=g++ \
  -DCMAKE_CXX_FLAGS="-I/usr/include" \
  -DBoost_NO_BOOST_CMAKE=ON \
  -DBoost_DEBUG=ON \
  -DBoost_USE_STATIC_LIBS=OFF \
  -DBoost_USE_DEBUG_LIBS=OFF \
  -DBoost_USE_RELEASE_LIBS=ON \
  -DBoost_USE_MULTITHREADED=ON \
  -DBoost_INCLUDE_DIR="$CONDA_PREFIX/include" \
  -DBoost_LIBRARY_DIR_RELEASE="$CONDA_PREFIX/lib" \
  -DBoost_FILESYSTEM_LIBRARY_RELEASE="$CONDA_PREFIX/lib/libboost_filesystem.so" \
  -DBoost_SYSTEM_LIBRARY_RELEASE="$CONDA_PREFIX/lib/libboost_system.so" \
  -DXERCES_INCLUDE_DIR="$CONDA_PREFIX/include" \
  -DXERCES_LIBRARY="$CONDA_PREFIX/lib/libxerces-c.so" \
  -DXSD_EXECUTABLE="/usr/bin/xsdcxx" \
  -DXSD_INCLUDE_DIR="/usr/include"

```

使用WSL系統
加入
```bash
nano /root/CEINMS/lib/InputConnectors/FromStorageFile/Utilities.cpp
#include <iostream>
#include <algorithm>  // for std::remove_if, std::find, etc.
#include <iterator>   // for std::begin, std::end

```

```bash
rm -rf build
mkdir build
cd build

cmake .. \
  -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_C_COMPILER=/usr/bin/gcc \
  -DCMAKE_CXX_COMPILER=/usr/bin/g++ \
  -DCMAKE_CXX_FLAGS="-I/usr/include" \
  -DBoost_NO_BOOST_CMAKE=ON \
  -DBoost_USE_STATIC_LIBS=OFF \
  -DBoost_USE_MULTITHREADED=ON \
  -DBoost_USE_DEBUG_LIBS=OFF \
  -DBoost_USE_RELEASE_LIBS=ON \
  -DBoost_INCLUDE_DIR="/usr/include" \
  -DBoost_LIBRARY_DIR_RELEASE="/usr/lib/x86_64-linux-gnu" \
  -DXSD_EXECUTABLE="/usr/bin/xsdcxx" \
  -DXSD_INCLUDE_DIR="/usr/include" \
  -DXERCES_INCLUDE_DIR="/usr/include" \
  -DXERCES_LIBRARY="/usr/lib/x86_64-linux-gnu/libxerces-c.so"

make -j4
```

使用的版本跟windows上的不一樣，opensim要用linux
用wine
```
sudo apt install wine64
sudo apt install wine32
wine ./installer
需要opensim3.3, CEINMS
```
[How to Install Wine on Ubuntu {Tutorial with Screenshots}](https://phoenixnap.com/kb/how-to-install-wine-on-ubuntu#wine-start-command)
```
alias WINE_CEINMS='wine "~/.wine/drive_c/Program Files/CEINMS 0.10/bin/CEINMS.exe"'
```