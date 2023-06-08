# PotreeConverter + PROJ4

[https://knowledge.informatica.com/s/article/HOW-TO-Build-Libcurl-Libraries-for-Windows-and-Linux-for-Data-Archive?language=en_US](https://knowledge.informatica.com/s/article/HOW-TO-Build-Libcurl-Libraries-for-Windows-and-Linux-for-Data-Archive?language=en_US)

Dependancies:

- libtiff
- SQLite3
- proj4

### Requirements

- Git
- Perl
- Visual Studio
- CMake

Make sure to install each of the above dependancies.

Also make sure you have the PotreeConverter sources extracted.

### SQLite3 Compilation on Windows

1. Download the source code from https://github.com/alex85k/sqlite3-cmake
2. Extract the contents of the downloaded file to a directory of your choice.
3. Open the "Developer Command Prompt for Visual Studio" and navigate to the directory where the SQLite3 source code was extracted.
4. Run the following command to generate the VS solution files (you can change the install_prefix to a desired directory):
    
    ```
    cmake -G "NMake Makefiles" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=d:/libs
    nmake install
    ```
    
5. Copy the whole content of the built folder to PotreeConverter/Converter/libs/sqlite3/libs

### Libtiff Compilation on Windows

1. Download the source code from [https://download.osgeo.org/libtiff/](https://download.osgeo.org/libtiff/)
2. Extract the contents of the downloaded file to a directory of your choice.
3. Open the "Developer Command Prompt for Visual Studio" and navigate to the directory where the libtiff source code was extracted. Go to the build folder.
4. Run the following commands to generate the VS solution files:
    
    ```
    cd build
    cmake ..
    
    ```
    
5. Open the tiff.sln solution and compile the whole solution in Release mode.
6. Copy the following files to PotreeConverter/Converter/libs/libtiff:
    
    ```
    tiff.lib
    tiff.dll
    tiff.exp
    tiff.h
    ```
    

### Building Libcurl Libraries for Windows

Download the following files:

- OpenSSL 1.1.1k ( [https://ftp.openssl.org/source/old/1.1.1/openssl-1.1.1k.tar.gz](https://ftp.openssl.org/source/old/1.1.1/openssl-1.1.1k.tar.gz))
- Libssh2 1.9.0 ( [https://www.libssh2.org/download/libssh2-1.9.0.tar.gz](https://www.libssh2.org/download/libssh2-1.9.0.tar.gz))
- Curl 7.74.0 ( [https://curl.se/download/curl-7.74.0.zip](https://curl.se/download/curl-7.74.0.zip))
- Cmake ([https://cmake.org/files/v3.18/cmake-3.18.0-rc1-win64-x64.zip](https://cmake.org/files/v3.18/cmake-3.18.0-rc1-win64-x64.zip))

Run the following commands:

- mkdir openssl
- mkdir libssh2
- mkdir libcurl

To create the libraries, perform the following tasks:

1. Extract the openssl-1.1.1k.tar.gz file.
2. Extract the openssl-1.1.1k.tar file.
3. Open a command prompt for Visual Studio Native tools x64 from the following location.
4. Run the following commands:
    1. cd openssl-1.1.1k
    2. perl Configure VC-WIN64A -no-asm --prefix=<output directory path> --openssldir=<output directory path>
    3. nmake
    4. nmake install
5. Copy libcrypto.lib, libssl.lib, libcrypto-1_1-x64.dll, and libssl-1_1-x64.dll to the openssl folder.
6. Copy the contents of <output directory path>/include to the openssl folder.
7. Extract the libssh2-1.9.0.tar.gz file.
8. Extract the libssh2-1.9.0.tar file.
9. Navigate to the following directory: libssh2-1.9.0
10. Run the following command:cmake -DCRYPTO_BACKEND=OpenSSL -DBUILD_SHARED_LIBS=ON -DOPENSSL_INCLUDE_DIR=<FULL_DIR_PATH>/openssl -DOPENSSL_ROOT_DIR=<FULL_DIR_PATH>/openssl/include
11. Open Visual Studio 2019 and perform the following steps:

a. Click File->Open and select libssh2 project.

b. Open Configuration Manager.

[https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3Zw](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3Zw)

c. Click Active solution Platform.

[https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3Zr](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3Zr)

d.

d. Create a new solution platform for x64.

[https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3b4](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3b4)

e. Navigate to libssh2 project and select Properties.

f. Click Linker-> Additional Library Directories.

[https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3cI](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3cI)

g. Add the location <FULL_DIR_PATH>/openssl to the Additional Library Directories.

h. Click Input->Additional Dependencies.

[https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3hC](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3hC)

i. Remove ssleay32.lib and libeay32.lib and add libssl.lib and libcrypto.lib.

j. Click Linker->Command Line.

k. Remove /machine:x86 from Additional Options.

[https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3ex](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3ex)

l. After applying the changes, build the libssh2 project.

1. Copy the libssh2.lib file from <FILE_PATH>\libssh2-1.9.0\src\Release to libssh2.
2. Copy the libssh2.dll from <FILE_PATH>\libssh2-1.9.0\x64\Release to libssh2.
3. Copy <FILE_PATH>\libssh2-1.9.0\include to libssh2.
4. Extract the curl-7.74.0.tar.gz file.
5. Extract the curl-7.74.0.tar file.
6. Browse to the following location: curl-7.74.0 -> projects->Windows->VC15.
7. Open the curl-all.vcxproj and perform the following steps:
    1. Retarget the libcurl project to the latest SDK version.

[https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3ij](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3ij)

1. b. Change the configuration of the libcurl project to DLL Release – DLL OpenSSL – DLL LibSSH2.’
2. c. Click Solution Platform.
3. 
4. 
    
    [https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3kV](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3kV)
    

d. Choose Configuration Manager -> Active Solution platform.

1. e. Create a new solution platform for x64.
2. 
    
    [https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3mW](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3mW)
    
3. f. Navigate to Properties for the libcurl project.
4. g. Add <FILE_PATH>/openssl/include and <FILE_PATH>/libssh2/include to Additional Include Directories.
5. 
    
    [https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3nF](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3nF)
    
6. h. Click Linker -> General.
7. i. Add <FILE_PATH>\openssl and <FILE_PATH>\libssh2 to Additional Library Directories.
8. 
    
    [https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3nt](https://knowledge.informatica.com/servlet/rtaImage?eid=ka06S000000Yveg&feoid=00N3f000000ZgGS&refid=0EM6S000004L3nt)
    
9. j. Navigate to Linker -> Input -> Additional Dependencies and remove ssleay32.lib and libeay32.lib. Add libssl.lib and libcrypto.lib.
10. k. Save the properties build the libcurl project.
11. Copy libcurl.lib and libcurl.dll from <FILE_PATH>\curl-7.74.0\build\Win64\VC15\DLL Release - DLL OpenSSL - DLL LibSSH2 to libcurl.
12. Copy all the lib and dll files from openssl, libssh2 and libcurl to PotreeConverter/Converter/libs/libcurl/libs.
    1. libcrypto.lib
    2. libcrypto-1_1-x64.dll
    3. libssl.lib
    4. libssl-1_1-x64.dll
    5. libssh2.lib
    6. libssh2.dll
    7. libcurl.lib
    8. libcurl.dll
13. Copy all \include\curl folder to PotreeConverter/Converter/libs/libcurl/include

### Building proj4 library for Windows

1. Download latest release from [https://proj.org/en/9.2/download.html](https://proj.org/en/9.2/download.html)
2. Run the following command from within the extracted proj folder (by replacing the paths matching your own.)

```jsx
cmake -DSQLITE3_INCLUDE_DIR=<C:\PotreeConverter\Converter\libs\sqlite3\includes> -DSQLITE3_LIBRARY=<C:\PotreeConverter\Converter\libs\sqlite3\libs> -DEXE_SQLITE3=<C:\PotreeConverter\Converter\libs\sqlite3\bin> -DTIFF_INCLUDE_DIR=<C:\PotreeConverter\Converter\libs\libtiff> -DTIFF_LIBRARY=<C:\PotreeConverter\Converter\libs\libtiff\tiff.lib> -DCURL_LIBRARY=<C:\PotreeConverter\Converter\libs\libcurl\libs\libcurl.lib> -DCURL_INCLUDE_DIR=<C:\PotreeConverter\Converter\libs\libcurl\include> ..
```

Rebuild