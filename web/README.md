# Web apps
This sample produces an image that installs required framework and workloads for web app authoring.

We start from the microsoft/dotnet-framework:3.5-sdk-windowsservercore-1709 base image for consistency with the managed-native-desktop sample. We use RS3 because the same image can be used on Windows Server 2016 nodes that do not yet support RS4 containers.

On top of that we add the workloads for building .NET and .NET Core apps. Also add environment variables that point to the `msbuild` and extensions paths. These are used in `.csproj` files to `find` the location of tools.

## Building
To build this image from this directory, run:

```batch
docker build -t buildtools2017web:latest -m 2GB .
```
## Running with CAKE
Assuming CAKE is used then a `build.ps1` script should be available. It can be run using the following command from a clean source repository:

```batch
docker run -m 2G ^
 -v %CD%:c:\src ^
 -w c:\src ^
 buildtools2017web:latest ^
 powershell .\build.ps1 -Target="Default" -Transform="Debug" -Configuration="Debug
```
 - runs `buildtools2017web:latest` and passes in the current working directory `%CD%` and designates it `c:\src` 'inside' the container
 - designates the working directory to `c:\src`
 - starts the `build.ps1` script (in this instance with a debug config)

## Running
To map and build web sources from a clean source repository, run:

```batch
docker run -m 2G -v %CD%:C:\src buildtools2017web:latest --name Solution msbuild /m c:\src\Solution.sln
```

You can optionally pass specific configurations to build as well.

```batch
docker run -m 2G -v %CD%:C:\src buildtools2017web:latest --name Solution msbuild /m c:\src\Solution.sln /p:Configuration=Debug /p:Platform=x64
```

To build again run the container created in the previous step, e.g.
```batch
docker start -a Solution
```

You can omit the -a that attaches the container to view the output if desired.

## Issues

* If the repository is not clean and the mapped directory is not on the same drive or the same path as the host directory, web project builds will fail with a front-end compiler error.
* The compile flag /CI causes a compiler error when used in a container. In your project properties under C/C++ change Debug Information Format to C7 compatible when building in a container.
