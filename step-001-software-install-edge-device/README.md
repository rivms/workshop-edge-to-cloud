# Azure IoT Edge Device Software Installation
An Ubuntu 18.04 vm has been provisioned in each resource group. The installation steps will be run on this machine via ssh.  

## Learning Goals
* Edge device remote access via ssh  
* Install moby engine
* Install IoT Edge runtime components
* Installed software check

## Resources
* [IoT Edge runtime architecture](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-runtime)
* [Security manager architecture](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-security-manager)
* [IoT Edge OSS project](https://github.com/Azure/iotedge)

## Steps
* [Configure apt repository](#repository-configuration)
* [Install a container engine](#install-moby)
* [Install IoT Edge security manager](#install-iot-edge-security-manager)
* [Check installation](#check-installation)
### Repository Configuration
Perform the steps for your linux distribution
1. [Ubuntu 18.04](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?tabs=linux#prerequisites)

### Install Moby
The [Moby](https://mobyproject.org/) engine is the  officially supported container engine for Azure IoT Edge
1. [Moby runtime installation steps](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?tabs=linux#install-a-container-engine) 

### Install IoT Edge Security Manager
The security manager is comprised of three key components whose primary responsibility from an installation perspective is boostrapping the IoT Edge runtime components
1. [Installtion steps](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?tabs=linux#install-the-iot-edge-security-daemon)

### Check Installation
At this stage the IoT Edge runtime has been installed but not configured. Errors in the logs are expected so the steps below validate only that the required components are now available for use.
1. Moby installation check
```
sudo docker version
```
![Moby Version](assets/moby-version.png)
1. IoT edge runtime configuration check. A cli tool, iotedge, is provided to assist with querying and validating the state of the install edge runtime. Configuration errors are expected to be reported
```
sudo iotedge check
```
![iotedge check](assets/iotedge-check.png)
1. Security daemon status check. The security daemon is currently in a failed state as it's configuration file has not been populated as yet.
```
systemctl status iotedge
```
![systemctl status](assets/systemctl-iotedge.png)
1. Security daemon logs. The logs again show that the configuration file, config.yaml, has not been updated.
```
journalctl -u iotedge
```
![journalctl status](assets/journalctl-iotedge.png)