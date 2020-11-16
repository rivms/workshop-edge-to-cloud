# Getting Started

A shared Azure Subscription has been setup for attendees. This section describes the steps to access the environment as well as setting up your laptop for the steps that follow.

## Learning Goals
* Access Azure Portal
* Download tools


## Steps
* [Clone Repo](#clone-repo)
* [Access Azure Portal](#access-azure-portal)
* [Download Tools](#download-tools)
* [Install Azure IoT Explorer](#azure-iot-explorer)

### Clone Repo
This repository includes a working folder "labs" that is assumed to be the current folder for executing tools and scripts from the command line. 
1. Clone this repository to a folder on your development machine
   ```
   git clone https://github.com/rivms/workshop-edge-to-cloud.git
   ```
1. Change directory to the "labs" folder

### Access Azure Portal
1. Visit the [Azure Portal](https://portal.azure.com)
1. Sign-in using your assigned credentials
1. You will have access to a single resource group


### Download Tools

|App|Steps|Comments|
|---|-----|--------|
|[Azure IoT Explorer](#azure-iot-explorer)|[download](https://docs.microsoft.com/en-us/azure/iot-pnp/howto-use-iot-explorer)|Desktop app for observing IoT Hub instances|
|Azmsg CLI|[download](https://github.com/rivms/msgtool/releases)|CLI tool, helps with sending and viewing messages|
|SSH / Putty||SSH client used to access the Edge Device VM|
|VS Code||IDE for development as well as inspecting Azure resources|


#### Azure IoT Explorer
Follow the instructions availabe [here](https://docs.microsoft.com/en-us/azure/iot-pnp/howto-use-iot-explorer) to download and install. When running the tool the inital screen will appear similar to the following screenshot. 
![screenshot](assets/azure-iot-explorer.png)




### VS Code
Once installed add the Azure IoT extensions
1. Download and install [VS Code](https://code.visualstudio.com/download)
2. Run VS Code and install the [Azure IoT Tools](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-tools) extension