<!--
The MIT License (MIT) 
Copyright (C) Microsoft Corporation. All rights reserved.
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
-->
# .NET Framework + native desktop
The Visual Studio setup engine builds both managed and native projects. Some managed projects even target .NET Framework 3.5 to provide a better downlevel experience where 4.5 is not (yet) present. Because of that, we start from the microsoft/dotnet-framework:3.5-sdk-windowsservercore-1709 base image. We use RS3 because the same image can be used on Windows Server 2016 nodes that do not yet support RS4 containers.

## Building
To build this image from this direectory, run:

```batch
docker build -t buildtools2017:latest -m 2GB .
```

## Running
To map and build managed and native sources from a clean source repository, run:

```batch
docker run -m 2G -v %CD%:C:\src buildtools2017:latest msbuild /m c:\src\Solution.sln
```

## Issues

* If the repository is not clean and the mapped directory is not on the same drive or the same path as the host directory, native project builds will fail with a front-end compiler error.
