# Exercise Prep
1. Verify Docker is installed and running on your system
    * ``` Powershell
       PS C:\Users\myuser> docker version
       Client: Docker Engine - Community
        Cloud integration: 1.0.12
        Version:           20.10.5
        API version:       1.41
        Go version:        go1.13.15
        Git commit:        55c4c88
        Built:             Tue Mar  2 20:14:53 2021
        OS/Arch:           windows/amd64
        Context:           default
        Experimental:      true

       Server: Docker Engine - Community
        Engine:
         Version:          20.10.5
         API version:      1.41 (minimum version 1.24)
         Go version:       go1.13.15
         Git commit:       363e9a8
         Built:            Tue Mar  2 20:26:56 2021
         OS/Arch:          windows/amd64
         Experimental:     false

2. Verify Docker is running in Windows Mode:
    ![Windows Run](https://github.com/lukearp/Windows-Linux-Container-Demo/blob/master/Windows/imgs/docker-mode.png?raw=true)

    If the option says Switch to Linux, you are running in Windows Mode.  If it says Switch to Windows, select to change to Windows Mode.

3. Verify Azure CLI is installed
    * ``` Powershell
      PS C:\Users\myUser> az version
      {
        "azure-cli": "2.22.1",
        "azure-cli-core": "2.22.1",
        "azure-cli-telemetry": "1.0.6",
        "extensions": {}
      }
4. Verify VSCode is installed
5. Download Windows-Linux Container Demo repository
    * ``` Powershell
      Invoke-WebRequest -Uri https://github.com/lukearp/Windows-Linux-Container-Demo/archive/refs/heads/master.zip -Method Get -OutFile Windows-Linux-Container-Demo.zip;
      Expand-Archive -Path .\Windows-Linux-Container-Demo.zip -DestinationPath .\;
      cd .\Windows-Linux-Container-Demo-master\;
      code .;
    If successful, VS Code should launch in the Directory of the project.  
6. Login to Azure CLI
    * ``` Powershell
      az login
7. Select Target Azure Subscription for Azure Container Registry
    * ``` Powershell
      az account set --subscription SUBSCRIPTION-ID
8. Create new Resource Group
    * ``` Powershell
      az group create --name RESOURCEGROUPNAME --location AZUREREGION
9. Create [Azure Container Registry (ACR)](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-intro)
    * ``` Powershell
      az acr create --resource-group RESOURCEGROUPNAME --name ACRNAME --sku Standard