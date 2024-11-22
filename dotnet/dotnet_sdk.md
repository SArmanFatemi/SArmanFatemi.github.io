# Install `dotnet` SDK on MAC (M3) using .NET Install Scripts

This guide provides step-by-step instructions for installing multiple .NET versions (3.1, 6, 7, 8) on your macOS (M3) using the official .NET Install Scripts.

## Step 0: Install Rosetta 2
First, ensure Rosetta 2 is installed:
```bash
/usr/sbin/softwareupdate --install-rosetta --agree-to-license
```

## Step 1: Download the .NET Install Script

1. Open the Terminal.
2. Download the installation script:
   ```bash
   curl -O https://dotnet.microsoft.com/download/dotnet/scripts/v1/dotnet-install.sh
   ```

## Step 2: Make the Script Executable

Make the downloaded script executable:

```bash
chmod +x dotnet-install.sh
```

## Step 3: Install .NET Versions

Run the following commands to install each .NET version:

- **.NET Core 3.1:**
```bash
./dotnet-install.sh --channel 3.1
```
- **.NET 6:**
```bash
./dotnet-install.sh --channel 6.0
```
- **.NET 7:**
```bash
./dotnet-install.sh --channel 7.0
```
- **.NET 8:**
```bash
./dotnet-install.sh --channel 8.0
```

## Step 4: Update Your Shell Profile

To make the `dotnet` command globally available, add the following line to your shell profile (e.g., `.zshrc`, `.bash_profile`):

```bash
export PATH="$HOME/.dotnet:$PATH"
```

Reload your shell profile:

```bash
source ~/.zshrc   # or source ~/.bash_profile if using bash
```

## Step 5: Verify the Installation

After installing each version, verify the installation:

```bash
dotnet --list-sdks
```

```bash
dotnet --list-runtimes
```
This commands should list the installed SDKs and Runtimes for the installed versions.

## Step 6: Confirm Installation

Verify that all .NET versions are correctly installed by running:

```bash
dotnet --info
```

This command will display detailed information about the installed .NET runtimes and SDKs.


# Uninstall `dotnet` completly

To completely remove .NET from your Mac, follow these steps. This process will delete all SDKs, runtimes, and associated files.
## Step 1: **Remove .NET SDK and Runtimes from Your User Directory**

Since `.NET` is installed in your home directory, you need to remove it from there. Run the following commands to delete all SDKs, runtimes, and other related files:

Remove the `.dotnet` directory where SDKs and runtimes are installed
```bash
sudo rm -rf /Users/seyedarmanfatemi/.dotnet
```

Optionally, remove the `NuGet` package cache (this stores libraries used by your projects)
```bash
sudo rm -rf /Users/seyedarmanfatemi/.nuget/packages
```
## Step 2: **Remove Any Symbolic Links**

If a symbolic link for `dotnet` was created in `/usr/local/bin/`, you can remove it with the following command:
```bash
sudo rm /usr/local/bin/dotnet
```


# Run `dotnet 3.1` on MAC
You'll need to configure `Rider` to use the `dotnet64` binary to compile your application. In version `2024.2.1` in the following path:
> Settings (⌘Сmd + ,) > Build, Execution, Deployment > Toolset and Build

Update the value of `.NET CLI executable path` to:
```bash
/usr/local/share/dotnet/x64/dotnet
```
Finally, save it only for the solution (not as a global setting, since it will break the execution of the newer version of the `dotnet`).

And If you're building your project outside of rider, you'll need an **alias** to an `x64` bit `dotnet` executable.
Put this in your **shell profile** (.zsh):

```zhs
alias dotnet64=/usr/local/share/dotnet/x64/dotnet
```

Then, when you open a terminal, you can execute a x64 build using:
```zsh
dotnet64 build myproj.csproj
```
