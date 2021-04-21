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
4. Login to Azure CLI
    * ``` Powershell
      az login
5. Select Target Azure Subscription for Azure Container Registry
    * ``` Powershell
      az account set --subscription SUBSCRIPTION-ID
6. Create new Resource Group
    * ``` Powershell
      az group create --name RESOURCEGROUPNAME --location AZUREREGION
7. Create [Azure Container Registry (ACR)](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-intro)
    * ``` Powershell
      az acr create --resource-group RESOURCEGROUPNAME --name ACRNAME --sku Standard
8. Assign [ACR Roles](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-roles) to users that will be managing containers:
   ![RBAC](https://github.com/lukearp/Windows-Linux-Container-Demo/blob/master/Windows/imgs/RBAC.PNG?raw=true)

# Builds
1. Login to ACR
    * ``` Powershell
      az acr login -n ACRNAME
2. Locally Build Container
    * ``` Powershell
      cd .\Builds\dotnetframework
      docker build -f Dockerfile.windowsservercore-ltcs2019 -t CONTAINERNAME:TAG .
3. Verify build is in Docker Images
    * ``` Powershell
      docker images
4. Run container Locally
    * ``` Powershell
      docker run -d -p 8080:80 CONTAINERNAME:TAG
5. Verify application is working by browsing to site: [Default Location](http://localhost:8080)
6. Tag container and push to ACR
    * ``` Powershell
      docker tag CONTAINERNAME:TAG ACRNAME.azurecr.io/CONTAINERNAME:TAG
      docker push ACRNAME.azurecr.io/CONTAINERNAME:TAG
7. Verify Repository is there:
    * ``` Powershell
      az acr repository list -n ACRNAME --output table

## Build with Azure CLI
1. Replace docker build with az acr build to offload to Azure Container Registry:
    * ``` Powershell
      az acr build -t ACRNAME.azurecr.io/CONTAINERNAME:TAG -r ACRNAME -f .\Dockerfile.windowsservercore-ltcs2019 --platform windows .
      az acr repository list -n ACRNAME --output table