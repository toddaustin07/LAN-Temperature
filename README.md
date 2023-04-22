# LAN Temperature & Humidity Driver
SmartThings Edge driver to support LAN-based apps to send temperature &amp; humidity to a SmartThings device via an HTTP POST request.

This driver requires my Edgebridge server to provide a fixed network address for the sending application to use, since the application cannot know the IP:Port address of the Edge driver running on the SmartThings hub.

The sending application (the application running on your LAN that will be sending the temperature and humidity readings) must provide the flexibility to define the HTTP method (POST) and URL use.  This driver will not work with applications that have fixed, or otherwise non-configurable URL formats.


## Prerequisites
* SmartThings Hub
* [Edgebridge server](https://github.com/toddaustin07/edgebridge)

## Installation
Enroll your hub in my test channel here.  Once enrolled, choose the **LAN Temp-Humidity Driver V1** from the list of drivers to install.

Once the driver is available on your hub, the next time you perform an Add device / Scan for nearby devices from the SmartThings app, a new device will be created and found in the Room where your hub device is located, called 'LAN Temp&Humdity Device'.

## Configuration
Open the LAN Temp&Humidity Device to the Controls screen and tap the vertical-3-dot menu icon in the upper right corner and select **Settings**.

Configure the options as follows:

* LAN Device Name - a short name that uniquely identifies this device, and will be included in the sending application's HTTP request
  - no special characters or blanks
* LAN App/Device Address - the IP address (and optionally port number) where the sending application is running
  - IP address only (e.g. '192.168.1.203'), or IP:Port address (e.g. '192.168.1.203:5643')
* Bridge Address - the IP:port address of Edgebridge (**MUST** include port number)
  - e.g. '192.168.1.150:8088'
* Received Temperature Unit - used to identify the temperature reading units as received from the sending application
  - Choose Celsius or Fahrenheit

## Sending application HTTP request format

The sending application must use the following format when sending the temperature or humidity readings to the Edge driver:

**POST http://\<*edgebridge address*\>/\<*devicename*\>/[temperature | humidity]/\<*reading*\>**

### Examples
Assume:
* Edgebridge server address is 192.168.1.150:8088
* LAN Device name configured in the SmartThings device is *mydevice*

#### Sending temperature
**POST http://192.168.1.150:8088/mydevice/temperature/25**

#### Sending humidity
**POST http://192.168.1.150:8088/mydevice/humidity/64**
