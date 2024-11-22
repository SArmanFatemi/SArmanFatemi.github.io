---
tags:
  - dotnet
  - dotnet_cli
---
**This article applies to:** ✔️ .NET Core 3.1 SDK and later versions

The _global.json_ file allows you to define which .NET SDK version is used when you run .NET CLI commands. Selecting the .NET SDK version is independent from specifying the runtime version a project targets. The .NET SDK version indicates which version of the .NET CLI is used. This article explains how to select the SDK version by using _global.json_.

If you always want to use the latest SDK version that is installed on your machine, no _global.json_ file is needed. In CI (continuous integration) scenarios, however, you typically want to specify an acceptable range for the SDK version that is used. The _global.json_ file has a `rollForward` feature that provides flexible ways to specify an acceptable range of versions. For example, the following _global.json_ file selects 6.0.300 or any later [feature band or patch](https://learn.microsoft.com/en-us/dotnet/core/releases-and-support) for 6.0 that is installed on the machine:
```json
{
  "sdk": {
    "version": "6.0.300",
    "rollForward": "latestFeature"
  }
}
```


# How to?
See which SDKs installed on your development environment:
```bash
dotnet --list-sdks
```

Choose your desire version and run (you can do this either in solution level or project level):
```bash
dotnet new globaljson --sdk-version 6.0.100
```


# Reference
https://learn.microsoft.com/en-us/dotnet/core/tools/global-json