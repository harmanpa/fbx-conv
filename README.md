fbx-conv
========

[![Build Status](https://travis-ci.org/libgdx/fbx-conv.svg?branch=master)](https://travis-ci.org/libgdx/fbx-conv)

Command line utility using the FBX SDK to convert [FBX/Collada/Obj files](http://docs.autodesk.com/FBX/2014/ENU/FBX-SDK-Documentation/files/GUID-0B122E01-7DB8-48E3-AADA-5E85A197FEE1.htm)
to more runtime friendly formats. The FBX content is parsed into an
in-memory datastructure. Pluggable writers then take this datastructure
to generate the output. Send us a pull request if you want the writer
for your engine/framework/app to be integrated. We'll build the
converter for Windows, Linux and Mac.

The FBX parser is largely based on GamePlay SDK's encoder. We'll try to
back-port any bug fixes or improvements.

Hangout notes https://docs.google.com/document/d/1nz-RexbymNtA4pW1B5tXays0tjByBvO8BJSKrWeU69g/edit#

Command-line Usage
====================
*   Windows - `fbx-conv-win32.exe [options] <input> [<output>]`
*   Linux - `fbx-conv-lin64 [options] <input> [<output>]`
*   Mac - `fbx-conv-mac [options] <input> [<output>]`

### Options/flags
*   **`-?`**				-Display help information.
*   **`-o <type>`**			-Set the type of the output file to `<type>` : FBX, G3DJ (json) or G3DB (binary).
*   **`-f`**				-Flip the V texture coordinates.
*   **`-p`**				-Pack vertex colors to one float.
*   **`-m <size>`**			-The maximum amount of vertices or indices a mesh may contain (default: 32k)
*   **`-b <size>`**			-The maximum amount of bones a nodepart can contain (default: 12)
*   **`-w <size>`**			-The maximum amount of bone weights per vertex (default: 4)
*   **`-v`**				-Verbose: print additional progress information

### Example
`fbx-conv-win32.exe -f -v myModel.fbx convertedModel.g3db`

Precompiled Binaries
====================

* [Mac](https://fbx-conv.s3.eu-west-2.amazonaws.com/mac/fbx-conv-mac.zip)
* [Linux 64](https://fbx-conv.s3.eu-west-2.amazonaws.com/linux/fbx-conv-linux.zip)
* [Windows](https://fbx-conv.s3.eu-west-2.amazonaws.com/win/fbx-conv.exe)


These binaries are recompiled on any changes in the Git repository, via the travis build

On Windows you'll need to install VC 2015 Redistributable Package https://www.microsoft.com/en-us/download/details.aspx?id=48145

On Linux and Mac, we have to link to the dynamic libraries of the FBX SDK (libfbxsdk.so and libfbxsdk.dylib). We recommend copying libfbxsdk.so
to /usr/lib on Linux. Otherwise you can use LD_LIBRARY_PATH and set it to the directory you put the .so file.

There's also a [Qt GUI wrapper](https://github.com/Reydw/Fbx-Converter-GUI) and [Java GUI](https://github.com/ASneakyFox/libgdx-fbxconv-gui) around it.

Building
========
You'll need premake and an installation of the FBX SDK 2019.0. Once installed/downloaded, set the
FBX_SDK_ROOT to the directory where you installed the FBX SDK. Then run one of the
generate_XXX scripts. These will generate a Visual Studio/XCode project, or a Makefile.

On Linux and Mac, you can follow [Travis build steps](.travis.yml) in order to build and run it.

Docker
======
Why not build your own docker image:

```bash
docker build . -t fbx-conv
```

Once done, run `fbx-conv` like this:

```bash
docker run --rm -v $PWD:/home fbx-conv my-model.obj
```
