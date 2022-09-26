## Adding company in the client tool mysql(same with mariadb) and the Windows installer
- This document assue the company name as ADS. 
- Source code update
```
> client tool : 
  - FILE : $SrcRoot/client/mysql.cc
  - FROM : put_info("Welcome to the MariaDB monitor.  Commands end with ; or \\g."
  - TO   : put_info("Welcome to the MariaDB monitor by ADS.  Commands end with ; or \\g."

> Windows installer
  - FILE : $SrcRoot/win/packaging/CMakeLists.txt
  - FROM : SET(CPACK_WIX_PACKAGE_NAME "MariaDB ${MAJOR_VERSION}.${MINOR_VERSION}")
  - TO   : SET(CPACK_WIX_PACKAGE_NAME "MariaDB ${MAJOR_VERSION}.${MINOR_VERSION} by ADS")
  - FROM : SET(CPACK_WIX_PACKAGE_NAME "MariaDB ${MAJOR_VERSION}.${MINOR_VERSION} (${WIX_ARCH})")
  - TO   : SET(CPACK_WIX_PACKAGE_NAME "MariaDB ${MAJOR_VERSION}.${MINOR_VERSION} by ADS (${WIX_ARCH})")
```



## Windows PATH adding
> C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin\cmake.exe
> C:\GnuWin32\bin\bison.exe & diff.exe

## Windows cmake
> install vcpkg
> install libraries using vcpkg
> Do according to comments in storage/oqgraph/cmake/FindJudy.cmake
   -  environment variable setting : JUDY_ROOT=C:\src\Judy-1.0.5
> use "Developer Command Prompt" instead of normal CMD
> set system locale to "United States" in control panel
> ## not working ## cmake ../server "-DCMAKE_TOOLCHAIN_FILE=C:\\src\\vcpkg\\scripts\\buildsystems\\vcpkg.cmake"
> cmake ../server "-DCMAKE_PREFIX_PATH=C:/src/vcpkg/installed/x86-windows" -DWITH_ROCKSDB_ZSTD=OFF
> cmake --build . --parallel 5
> cmake --build . --target MSI
> cmake --build . --config relwithdebinfo --target MSI
