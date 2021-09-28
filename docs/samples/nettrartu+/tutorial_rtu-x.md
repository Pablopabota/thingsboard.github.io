## Introduction

This guide contains instructions on how to connect your Nettra RTU-X to Thingsboard through MQTT via WiFi.

## Nettra RTU
[Nettra RTU-X](https://nettra.tech/en/how-we-do-it/rtu-x) is a powerful IoT gateway that has digital and analog inputs and outputs, as well as several integrated communication interfaces as wifi, modem, bluetooth, RS-485, etc.
It is an ideal product to implement monitoring, data acquisition and control applications over a distributed data network.

The RTU-X is configured using the [RTU-X User Interface](http://wiki.nettra.tech/en/downloads). To adapt the RTU-X to each application, it runs a fully customizable script, accessible and editable from the User Interface. In this guide we will provide a simple example.

### Connecting to the RTU-X

 Turn on the RTU-X and connect to the wifi network created by the RTU-X using the User Interface:

   1. Go to *"Home"*.
   2. Click on *"TCP/IP"*.
   4. Specify the *"IP*" address **"192.168.4.1"**, *"Port":* **"502"** (by default).
   5. Click on *"Connect"*.

   ![rtu1_step1](https://user-images.githubusercontent.com/61634031/134022796-78e22a93-5f03-4c9f-80bb-c129814b349a.png)

### WiFi Configuration

 - Once connected to the RTU-X, you need to configure the wifi network to connect to:
   1. Go to *"Communications"*.
   2. Go to *"Wifi, Serial, Modbus"*
   3. Check *"Station"* and enter the wifi network information 
   4. *"Apply Changes"*
   
   ![rtu3_step3](https://user-images.githubusercontent.com/61634031/134022912-8dcbe19c-986f-4fa7-8231-823564262343.png)
   
### MQTT Configuration

1. Go to *"Communications"*.
2. Click on *"MQTT"*.
3. On *"Interface"* select *"WiFi"*. On *"Format"* select *"Thingsboard"*. On *"URI"* paste *"mqtt://demo.thingsboard.io:1883"* (or the URI to your instance of Thingsboard). On *"Username"* paste the Device Acces Token from Thingsboard.
4. Click on *"Apply Changes"*.

![rtu5_step5](https://user-images.githubusercontent.com/61634031/134028854-17b5d9c8-c807-4b3b-a557-00ea5b25d7ac.png)

### Script

The script is where the variables are pushed to the cloud (among many other things!). Scripts can be very complex if required. Check out [Nettra Script User Manual](http://wiki.nettra.tech/en/script) for more information.
The following examples is just a simple one to illustrate the process, and it only sends a variable every 10 seconds and increments it.

1. Go to *"Script"* 
2. Paste the following script:
```c
// This variable can be anything, from an analogue input or register
// from a slave device
telemetry float variable = 0;

while (1)
{
    log(variable);
    variable = variable + 1;
    delay(10000);	// 10 seconds
}
```

3. Upload it by clicking *"Compile & Apply"*.

![rtu6_step6](https://user-images.githubusercontent.com/61634031/134028433-e7412285-9f4e-4d67-9f3c-80879f99191f.png)

## Thingsboard

You can now head to Thingsboard UI and find the device on the platform, where you will see the data coming in:

![dev](https://user-images.githubusercontent.com/61634031/134029353-d4d80304-0396-4a10-b313-02a249300280.png)

The following is a simple dashboard showing the latest value:

![dash](https://user-images.githubusercontent.com/61634031/134030076-19fd80de-38fd-4114-b1f1-221f61756782.png)

## See also

Browse other [samples](https://thingsboard.io/docs/samples/) or explore guides related to main ThingsBoard features:

 - [Device attributes](https://thingsboard.io/docs/user-guide/attributes/) - how to use device attributes.
 - [Data Visualization](https://thingsboard.io/docs/guides/#AnchorIDDataVisualization) - how to visualize collected data.
 - [Data Analytics](https://thingsboard.io/docs/guides/#AnchorIDDataAnalytics) - how to collect telemetry data.
 - [Rule Engine](https://thingsboard.io/docs/user-guide/rule-engine-2-0/re-getting-started/) - how to use rule engine to analyze data from devices.
 - [Using RPC capabilities](https://thingsboard.io/docs/user-guide/rule-engine-2-0/tutorials/rpc-request-tutorial/) - how to send commands to/from devices.
