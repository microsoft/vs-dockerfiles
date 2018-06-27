# Samples
You can install Visual Studio Build Tools [into a container](https://docs.microsoft.com/en-us/visualstudio/install/build-tools-container) to support a consistent, isolated build environment. This repository hosts a number of examples - and is accepting [contributions](CONTRIBUTING.md) for more, useful examples - you can use to build a container image using Build Tools tailored to your project types and build pipeline. Because these container images can be massive - larger than probably anyone needs - and the permutations of different Windows, Visual Studio, and .NET Framework versions would complicate which version you might need, you are encouraged to use these samples or build on them and publish, if desired, images to your own Docker registry on your LAN or WAN.

* [.NET Framework + native desktop](managed-native-desktop/README.md)

## Contributing
To contribute your own sample Dockerfiles and optional support scripts, please see [CONTRIBUTING](CONTRIBUTING.md).

## License
This project and all examples herein are licensed under the [MIT license](LICENSE.txt).
