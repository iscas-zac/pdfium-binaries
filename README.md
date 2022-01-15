# Pre-compiled binaries of PDFium

[![Build](https://github.com/bblanchon/pdfium-binaries/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/bblanchon/pdfium-binaries/actions/workflows/build.yml)
[![Total downloads](https://img.shields.io/github/downloads/bblanchon/pdfium-binaries/total)](https://github.com/bblanchon/pdfium-binaries/releases/)
[![Latest release](https://img.shields.io/github/v/release/bblanchon/pdfium-binaries?display_name=release&include_prereleases)](https://github.com/bblanchon/pdfium-binaries/releases/latest/)

This project hosts pre-compiled binaries of the [PDFium library](https://pdfium.googlesource.com/pdfium/), an open-source library for PDF manipulation and rendering.

Builds are triggered automatically every Monday since 2017.

**Disclaimer**: This project isn't affiliated with Google or Foxit.

## Download

Here are the download links for latest release:

<table>
  <tr>
    <th>OS</th>
    <th>CPU</th>
    <th>PDFium</th>
  </tr>

  <tr>
    <td rowspan="4">Android</td>
    <td>ARM</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-android-arm.tgz">pdfium-android-arm.tgz</a></td>
  </tr>
  <tr>
    <td>ARM64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-android-arm64.tgz">pdfium-android-arm64.tgz</a></td>
  </tr>
  <tr>
    <td>x64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-android-x64.tgz">pdfium-android-x64.tgz</a></td>
  </tr>
  <tr>
    <td>x86</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-android-x86.tgz">pdfium-android-x86.tgz</a></td>
  </tr>

  <tr>
    <td rowspan="2">iOS</td>
    <td>ARM64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-ios-arm64.tgz">pdfium-ios-arm64.tgz</a></td>
  </tr>
  <tr>
    <td>x64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-ios-x64.tgz">pdfium-ios-x64.tgz</a></td>
  </tr>

  <tr>
    <td rowspan="3">Linux</td>
    <td>ARM</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-linux-arm.tgz">pdfium-linux-arm.tgz</a></td>
  </tr>
  <tr>
    <td>ARM64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-linux-arm64.tgz">pdfium-linux-arm64.tgz</a></td>
  </tr>
  <tr>
    <td>x64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-linux-x64.tgz">pdfium-linux-x64.tgz</a></td>
  </tr>

  <tr>
    <td rowspan="2">macOS</td>
    <td>ARM64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-mac-arm64.tgz">pdfium-mac-arm64.tgz</a></td>
  </tr>
  <tr>
    <td>x64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-mac-x64.tgz">pdfium-mac-x64.tgz</a></td>
  </tr>

  <tr>
    <td rowspan="3">Windows</td>
    <td>ARM64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-win-arm64.tgz">pdfium-win-arm64.tgz</a></td>
  </tr>
  <tr>
    <td>x64</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-win-x64.tgz">pdfium-win-x64.tgz</a></td>
  </tr>
  <tr>
    <td>x86</td>
    <td><a href="https://github.com/bblanchon/pdfium-binaries/releases/latest/download/pdfium-win-x86.tgz">pdfium-win-x86.tgz</a></td>
  </tr>
</table>

See the [Releases page](https://github.com/bblanchon/pdfium-binaries/releases) to download older versions of PDFium.

## Documentation

### PDFium API documentation

Please find the [documentation of the PDFium API on developers.foxit.com](https://developers.foxit.com/resources/pdf-sdk/c_api_reference_pdfium/index.html).

### How to use PDFium in a CMake project

1. Unzip the dpwnloaded package in a folder (e.g., `C:\Libraries\pdfium`)
2. Set the environment variable `PDFium_DIR` to this folder (eg `C:\Libraries\pdfium`)
3. In your `CMakeLists.txt`, add

        find_package(PDFium)

4. Then link your executable with PDFium:

        target_link_libraries(my_exe pdfium)

5. On Windows, make sure that `pdfium.dll` can be found by your executable (copy it on the same folder, or put in on the `PATH`).

### How to use JavaScript V8 enabled binaries

If you are using the V8-enabled binaries, additional initialization is required.
In your code, before using PDFium you have to call `FPDF_InitEmbeddedLibraries()`
from the additional header `fpdf_libs.h`, which is only available in V8 enabled
binaries.

The archive will contain a `res` folder which you have to distribute with your
application. On macOS, you should include this in your application bundle for other
platforms place it where your application binary will find it.

See the following example for usage:

```c++
#include "fpdf_libs.h"

...

// Determine the path to files in the res folder from the archive
const char* resPath = "<path to the res folder>";

// Initialize V8 and other embedded libraries
FPDF_InitEmbeddedLibraries(resPath);

// Make use of PDFium
FPDF_InitLibrary();
FPDF_DestroyLibrary();
```

### How to create macOS universal binary

To  create a universal macOS binary containing both Intel and ARM code, download
both CPU versions and use the `mac_create_universal.sh` script to create a
universal archive.
