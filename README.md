# gdal.netcore

A simple (as is) build engine of [GDAL](https://gdal.org/) 3.1 library for [.NET Core](https://dotnet.microsoft.com/download). 

## Packages

NuGet: [MaxRev.Gdal.Core](https://www.nuget.org/packages/MaxRev.Gdal.Core/) <br/>

NuGet: [MaxRev.Gdal.LinuxRuntime.Minimal](https://www.nuget.org/packages/MaxRev.Gdal.LinuxRuntime.Minimal/) <br/>

NuGet: [MaxRev.Gdal.WindowsRuntime.Minimal](https://www.nuget.org/packages/MaxRev.Gdal.WindowsRuntime.Minimal/)

## Table Of Contents

- [gdal.netcore](#gdalnetcore)
  * [Table Of Contents](#table-of-contents)
  * [Packages](#packages)
  * [About this library](#about-this-library)
    + [What is this library](#what-is-this-library)
    + [What is not](#what-is-not)
  * [How to use](#how-to-use)
  * [How to compile on Windows](#how-to-compile-on-windows)
  * [How to compile on Unix](#how-to-compile-on-unix)
    
    + [Prerequisites](#prerequisites)
  * [Building runtime libraries](#building-runtime-libraries)
  * [Building Nuget Packages](#building-nuget-packages)
    + [Prerequisites](#prerequisites-1)
    + [Packaging](#packaging)
  * [FAQ](#faq)
      - [Missing {some} drivers, can you add more?](#q-missing-some-drivers-can-you-add-more)
      - [GDAL functions are not working as expected](#q-gdal-functions-are-not-working-as-expected)
      - [Some types throw exceptions from SWIG on Windows](#q-some-types-throw-exceptions-from-swig-on-windows)
      - [Can't compile on Windows](#q-cant-compile-on-windows)
      - [Can I compile it on Ubuntu or another unix-based system?](#q-can-i-compile-it-on-ubuntu-or-another-unix-based-system)
      - [In some methods performance is slower on Unix](#q-in-some-methods-performance-is-slower-on-unix)
  * [About and Contacts](#about-and-contacts)


## About this library

### What is this library

- Only generates assemblies and binds everything into one package.
- Provides easy access to GDAL by installing **only core and runtime package**
- DOES NOT require installation of GDAL 

### What is not

- Does not compile all drivers. Only configured, they are listed [below](#how-to-compile-on-unix). By default GDAL has a lot of internal drivers. 
- Does not change GDAL source code.
- Does not extend GDAL methods.

## How to use

1. Install core package - [MaxRev.Gdal.Core](https://www.nuget.org/packages/MaxRev.Gdal.Core/) 
 ```powershell
 Install-Package MaxRev.Gdal.Core
 ```
2. Install [libraries](#packages) for your runtime. You can install one of them or both with no conflicts. 
```powershell
Install-Package MaxRev.Gdal.Core.WindowsRuntime.Minimal
Install-Package MaxRev.Gdal.Core.LinuxRuntime.Minimal
```
3. Initialize libraries in runtime
```csharp
using MaxRev.Gdal.Core;
...
// call it once, before using GDAL
// this will initialize all GDAL drivers and set PROJ6 shared library paths
GdalBase.ConfigureAll();

```
4. Profit! Use it in ordinary flow


## How to compile on Windows

It's quite tricky. Enter [win](win/) directory to find out how.

## How to compile on Unix

Current version targets **GDAL 3.1.0** with **minimal drivers**

Drivers included PROJ6, SQLITE3, GEOS(3.8), HDF4, HDF5, GEOTIFF, JPEG, PNG, LIBZ, LERC, CURL

<details>
  <summary>Configure summary of current version</summary>

      GDAL is now configured for x86_64-pc-linux-gnu
      Installation directory:    /mnt/e/dev/builds/gdal-netcore/build-unix/gdal-build
      C compiler:                gcc -DHAVE_AVX_AT_COMPILE_TIME -DHAVE_SSSE3_AT_COMPILE_TIME -DHAVE_SSE_AT_COMPILE_TIME -fPIC -fvisibility=hidden
      C++ compiler:              g++ -DHAVE_AVX_AT_COMPILE_TIME -DHAVE_SSSE3_AT_COMPILE_TIME -DHAVE_SSE_AT_COMPILE_TIME -g -O2 -fvisibility=hidden
      C++14 support:             no
    
      LIBTOOL support:           yes
      
      LIBZ support:              internal
      LIBLZMA support:           no
      ZSTD support:              no
      cryptopp support:          no
      crypto/openssl support:    no
      GRASS support:             no
      CFITSIO support:           no
      PCRaster support:          no
      LIBPNG support:            internal
      DDS support:               no
      GTA support:               no
      LIBTIFF support:           internal (BigTIFF=yes)
      LIBGEOTIFF support:        internal
      LIBJPEG support:           internal
      12 bit JPEG:               yes
      12 bit JPEG-in-TIFF:       yes
      LIBGIF support:            no
      JPEG-Lossless/CharLS:      no
      OGDI support:              no
      HDF4 support:              yes
      HDF5 support:              yes
      Kea support:               no
      NetCDF support:            no
      Kakadu support:            no
      JasPer support:            no
      OpenJPEG support:          no
      ECW support:               no
      MrSID support:             no
      MrSID/MG4 Lidar support:   no
      JP2Lura support:           no
      MSG support:               no
      EPSILON support:           no
      WebP support:              no
      cURL support (wms/wcs/...):yes
      PostgreSQL support:        no
      LERC support:              yes
      MySQL support:             no
      Ingres support:            no
      Xerces-C support:          no
      Expat support:             no
      libxml2 support:           no
      Google libkml support:     no
      ODBC support:              no
      FGDB support:              no
      MDB support:               no
      PCIDSK support:            no
      OCI support:               no
      GEORASTER support:         no
      SDE support:               no
      Rasdaman support:          no
      DODS support:              no
      SQLite support:            yes
      PCRE support:              no
      SpatiaLite support:        no
      RasterLite2 support:       no
      Teigha (DWG and DGNv8):    no
      INFORMIX DataBlade support:no
      GEOS support:              yes
      SFCGAL support:            no
      QHull support:             no
      Poppler support:           no
      Podofo support:            no
      PDFium support:            no
      OpenCL support:            no
      Armadillo support:         no
      FreeXL support:            no
      SOSI support:              no
      MongoDB support:           no
      MongoCXX v3 support:       no
      HDFS support:              no
      TileDB support:            no
      userfaultfd support:       yes
      misc. gdal formats:        aaigrid adrg aigrid airsar arg blx bmp bsb cals ceos ceos2 coasp cosar ctg dimap dted e00grid elas envisat ers fit gff gsg gxf hf2 idrisi ignfheightasciigrid ilwis ingr iris iso8211 jaxapalsar jdem kmlsuperoverlay l1b leveller map mrf msgn ngsgeoid nitf northwood pds prf r raw rmf rs2 safe saga sdts sentinel2 sgi sigdem srtmhgt terragen til tsx usgsdem xpm xyz zmap rik ozi grib eeda plmosaic rda wcs wms wmts daas rasterlite mbtiles pdf
      disabled gdal formats:
      misc. ogr formats:         aeronavfaa arcgen avc bna cad csv dgn dxf edigeo geoconcept georss gml gmt gpsbabel gpx gtm htf jml mvt ntf openair openfilegdb pgdump rec s57 segukooa segy selafin shape sua svg sxf tiger vdv wasp xplane idrisi pds sdts amigocloud carto cloudant couchdb csw elastic gft ngw plscenes wfs gpkg vfk osm
      disabled ogr formats:
      
      SWIG Bindings:             no
      
      PROJ >= 6:                 yes
      enable GNM building:       no
      enable pthread support:    yes
      enable POSIX iconv support:yes
      hide internal symbols:     yes
</details>

**NOTE**: Windows and Linux drivers availability may differ, ask me of specific driver for runtime. Please issue, if I forgot to mention any other packages.

## Building runtime libraries

Current version is targeting GDAL 3.1.0 version. Each runtime has to be build separately, but this can be done concurrently as they are using different contexts (build folders). Main operating bindings (in gdalcore package) are build from **linux**.

To make everything work smoothly, each configuration targets same drivers and their versions respectively.

- Configuration files of unix runtime - `unix/GdalCore.opt`
- Configuration of windows runtime - `win/CONFIGVARS.bat`
- - Patched configuration - `win/presource/gdal-nmake.opt` 
  - Patched makefile - `win/presource/gdal-makefile.vc`

To build for a specific runtime, see the **README.md** in respective directory.

## Building Nuget Packages

### Prerequisites

1. Install [.NET Core SDK](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/install)  and [Nuget.exe](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) - for building and publishing packages
2. You have already built everything 

### Packaging

1. I'm using debian for example:

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget -q https://packages.microsoft.com/config/debian/9/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
sudo apt-get install apt-transport-https && apt-get update && apt-get install dotnet-sdk-2.2
```

2. And then just 

```shell
make pack
```

## FAQ

#### Q: Missing {some} drivers, can you add more?

A: Feel free to contribute and I will help you you to add them. Here's the my additional [answer](https://github.com/MaxRev-Dev/gdal.netcore/issues/8#issuecomment-569864199).

#### Q: GDAL functions are not working as expected

A: Try to search an [issue on github](https://github.com/OSGeo/gdal/issues). In 98% cases, I'm sure they are working fine.  

#### Q: Some types throw exceptions from SWIG on Windows

A: Yes, currently there are [some redundant](https://github.com/MaxRev-Dev/gdal.netcore/issues/11) types in OGR namespace. This will be fixed in the next builds.

#### Q: Can't compile on Windows

A: I've built it on my machine several times from scratch. Do you have installed all SDKs? If you know **cmake** or **nmake** [you can help to port](https://github.com/MaxRev-Dev/gdal.netcore/projects/1) batch files that are buggy.

#### Q: Can I compile it on Ubuntu or another Unix-based system?

A: The main reason I'm compiling it on CentOS - glibc of version 2.17. It's the lowest version [(in my opinion)](https://github.com/MaxRev-Dev/gdal.netcore/issues/1#issuecomment-522817778) that suits for all common systems (Ubuntu, Debian, Fedora)

#### Q: In some methods performance is slower on Unix 

A: Use of [older version](https://github.com/MaxRev-Dev/gdal.netcore/issues/1) of GLIBC might be [a reason](https://github.com/MaxRev-Dev/gdal.netcore/issues/6). But It's not a fault of build engine.


## About and Contacts

based on https://github.com/OSGeo/gdal && https://github.com/jgoday/gdal

Contact me: [Telegram - MaxRev](http://t.me/maxrev)

Enjoy!
