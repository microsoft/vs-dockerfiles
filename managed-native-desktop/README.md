# .NET Framework + native desktop
The Visual Studio setup engine builds both managed and native projects. Some managed projects even target .NET Framework 3.5 to provide a better downlevel experience where 4.5 is not (yet) present. Because of that, we start from the microsoft/dotnet-framework:3.5-sdk-windowsservercore-1709 base image. We use RS3 because the same image can be used on Windows Server 2016 nodes that do not yet support RS4 containers.

## Building
To build this image from this direectory, run:

```batch
docker build -t buildtools2022:latest -m 2GB .
```

## Running
To map and build managed and native sources from a clean source repository, run:

```batch
docker run -m 2G -v %CD%:C:\src buildtools2022:latest msbuild /m c:\src\Solution.sln
```

## Issues

* If the repository is not clean and the mapped directory is not on the same drive or the same path as the host directory, native project builds will fail with a front-end compiler error.
