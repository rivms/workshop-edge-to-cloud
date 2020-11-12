# Azure IoT Edge Configuration
Azure IoT Edge enables a hybrid architecture by providing a secure, container based solution deployed at edge locations and integrating with a cloud based gateway, IoT Hub, that provides edge and leaf device management, bidrectional communication and edge compute orchestration. To get started the initial installation of the Azure IoT Edge runtime software includes a sample configuration file "/etc/iotedge/config.yaml". The default values provided by the installer are sufficient to get started with minimumal additional configuration. The bootstrap or provisioning process relies on connecting with the IoT Hub instance that will manage the edge device. 

To complete this configuration goal two approaches are available:
- Supplying connection details for the IoT Hub
- Just in time provisioning via the [Azure IoT Hub Device Provisioning Service](https://docs.microsoft.com/en-us/azure/iot-dps/) 

A just in time provisioning process offers a scalable approach for the configuration of multiple edge devices which is the approach used in this section. 

## Learning Goals
* Edge device configuration  
* Just in time provisioning
* Edge device attestation
* Edge device configuration check

## Resources
* [Symmetric key attestation](https://docs.microsoft.com/en-us/azure/iot-dps/concepts-symmetric-key-attestation?view=iotedge-2018-06)
* [Deriving device keys for a group enrollment](https://docs.microsoft.com/en-us/azure/iot-dps/how-to-use-custom-allocation-policies#derive-unique-device-keys)
* [Using custom allocation policies](https://docs.microsoft.com/en-us/azure/iot-dps/tutorial-custom-allocation-policies?view=iotedge-2018-06&tabs=powershell)

## Steps
* [Review configuration file](#review-configuration)
* [Deriving Symmetric Key for an Edge Device](#deriving-symmetric-key)
* [Install IoT Edge security manager](#install-iot-edge-security-manager)
* [Check installation](#check-installation)
### Repository Configuration
Perform the steps for your linux distribution
1. [Ubuntu 18.04](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?tabs=linux#prerequisites)

### Review Cofiguration
The inital configuration file is located at "/etc/iotedge/config.yaml". 
1. Connect to the virtual machine via ssh. The details for connecting to the virtual machine can be found via the portal. 
![ssh](assets/connect-ssh.gif)
1. The ssh key can be downloaded from the resource url shared at the session
1. Once connected mount the shared folder by running the commang below. The shared files will be used later in this section 
   ```
   sudo mount -a
   ``` 

1. The IoT Edge config file can now be viewed using the command below. No changes are needed just yet, browse the file and familiarise yourself with its structure
   ```
   sudo nano /etc/iotedge/config.yaml
   ``` 
   ![config yaml](assets/config.png)



### Deriving Symmetric Key


The Azure DPS symmetric key provisioning method will be used. This requires three pieces of information:
- A scope id
- A registration id
- A symmetric key derived using the registration id and the group enrollment key


Once configured the IoT Edge security daemon will on startup connect to the Azure Device Provisioning Service and be assigned an IoT Hub instance to connect this. This allows at scale provisioning which in this scenario leverages an Azure Function that determines the IoT Hub instance to use. The logic to determine the IoT Hub instance simply examines the edge vms name and uses the numbered suffix to select an IoT Hub instance with a similar suffix.

1. The scope id will be provided in the session
1. The registration id is the edge device identifier that will be seen in IoT Hub. It is recommended that the vm name be used as the registration id
1.  The symmetric key needs to be derived using the registration id and group enrollment key (also provided in the session)
![device key](assets/key-diversification.png)
1. Steps to derive key here ...
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