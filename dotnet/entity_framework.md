---
tags:
  - dotnet
  - entity-framework
  - ef-tool
---
≤# Installing the tools

`dotnet ef` can be installed as either a global or local tool. Most developers prefer installing `dotnet ef` as a global tool using the following command:

.NET CLICopy

```bash
dotnet tool install --global dotnet-ef
```

To use it as a local tool, restore the dependencies of a project that declares it as a tooling dependency using a [tool manifest file](https://learn.microsoft.com/en-us/dotnet/core/tools/global-tools#install-a-local-tool).

Update the tool using the following command:

.NET CLICopy

```bash
dotnet tool update --global dotnet-ef
```

# Useful commands
```bash
dotnet ef database update
```
```bash
dotnet ef migrations add MIGRATION_NAME
```
```bash
dotnet ef migrations remove
```
```bash
dotnet ef migrations remove --context DBCONTEXT_NAME
```