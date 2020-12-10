<!--
The MIT License (MIT) 
Copyright (C) Microsoft Corporation. All rights reserved.
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
-->
# Native desktop
This sample produces an image that installs native C/C++ support only. It installs the core VC Tools workload with recommended components that include CMake and the Windows SDK. See our documentation for [additional workloads and components](http://aka.ms/vs/workloads) you can use.

We start from the microsoft/dotnet-framework:3.5-sdk-windowsservercore-1709 base image for consistency with the managed-native-desktop sample. We use RS3 because the same image can be used on Windows Server 2016 nodes that do not yet support RS4 containers.

## Building
To build this image from this directory, run:

```batch
docker build -t buildtools2017native:latest -m 2GB .
```

## Running
To map and build native sources from a clean source repository, run:

```batch
docker run -m 2G -v %CD%:C:\src buildtools2017native:latest --name Solution msbuild /m c:\src\Solution.sln
```

You can optionally pass specific configurations to build as well.

```batch
docker run -m 2G -v %CD%:C:\src buildtools2017native:latest --name Solution msbuild /m c:\src\Solution.sln /p:Configuration=Debug /p:Platform=x64
```

To build again run the container created in the previous step, e.g.
```batch
docker start -a Solution
```

You can omit the -a that attaches the container to view the output if desired.

## Issues

* If the repository is not clean and the mapped directory is not on the same drive or the same path as the host directory, native project builds will fail with a front-end compiler error.
* The compile flag /CI causes a compiler error when used in a container. In your project properties under C/C++ change Debug Information Format to C7 compatible when building in a container.
