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
