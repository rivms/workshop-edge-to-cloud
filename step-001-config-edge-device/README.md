# Configuring an Azure IoT Edge Device
A shared Azure Subscription has been setup for attendees. This section describes the steps to access the environment as well as setting up your laptop for the steps that follow.

## Learning Goals
* Access Azure Portal
* Awareness of useful development tools

## Resources
* [IoT Edge runtime architecture](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-runtime)
* [Security manager architecture](https://docs.microsoft.com/en-us/azure/iot-edge/iot-edge-security-manager)
* [IoT Edge OSS project](https://github.com/Azure/iotedge)

## Steps
* [Configure apt repository](#repository-configuration)
* [Install a container engine](#install-moby)
* [Install IoT Edge security manager](#install-iot-edge-security-manager)

### Repository Configuration
Perform the steps for your linux distribution
1. [Ubuntu 18.04](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?tabs=linux#prerequisites)

### Install Moby
The [Moby](https://mobyproject.org/) engine is the only container engine officially supported with Azure IoT Edge
1. [Moby runtime installation steps](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?tabs=linux#install-a-container-engine) 

### Install IoT Edge Security Manager
The security manager is comprised of three key components whose primary responsibility from an installation perspective is boostrapping the IoT Edge runtime components
1. [Installtion steps](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?tabs=linux#install-the-iot-edge-security-daemon)
