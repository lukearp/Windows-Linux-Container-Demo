# What do I need?
## Windows Container Builds
* Have CPU Virtualization enabled on your Bios
* Windows 10 Pro version 1903 or higher
* Hyper-V Setup - [Enable Hyper-V on Windows 10 | Microsoft Docs](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v#:~:text=Enable%20the%20Hyper-V%20role%20through%20Settings%201%20Right,or%20off.%204%20Select%20Hyper-V%20and%20click%20OK.) – this command should be all you need: 
```Powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```
* Azure CLI: [AZ CLI Install](https://aka.ms/installazurecliwindows)

## Linux Container Builds
* Have CPU Virtualization enabled on your Bios
* Windows 10 Pro version 1903 or higher
* WSL 2 Setup - [Install Windows Subsystem for Linux (WSL) on Windows 10 | Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

## Docker Install
* [Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)

## Install VSCode
* [VS Code](https://code.visualstudio.com/Download#)

## Download Repository
* ``` Powershell
      Invoke-WebRequest -Uri https://github.com/lukearp/Windows-Linux-Container-Demo/archive/refs/heads/master.zip -Method Get -OutFile Windows-Linux-Container-Demo.zip;
      Expand-Archive -Path .\Windows-Linux-Container-Demo.zip -DestinationPath .\;
      cd .\Windows-Linux-Container-Demo-master\;
      code .;
    If VS Code installed, program should launch in the Directory of the project.