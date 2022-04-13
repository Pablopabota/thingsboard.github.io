---
layout: docwithnav
title: Data upload over MQTT using Nettra RTU-X
description: ThingsBoard IoT Platform sample for data upload over MQTT using Nettra RTU-X
hidetoc: "true"
---

## Table of contents
1. [Introduction](#introduction)
3. [Prerequisites](#prerequisites)
4. [Connection diagram](#connection_diagram)
5. [ThingsBoard configuration](#tb_configuration)
6. [Connect RTU-X to PC](#connection_pc)
7. [RTU-X configuration](#rtu_configuration)
8. [Data visualization](#data_visualization)

## Introduction <a name="introduction"></a>

This guide contains step-by-step instructions on how to connect your Nettra RTU-X device to ThingsBoard through TCP/IP via WiFi. At the end of this guide, you will be able to monitor data using Thingsboard web UI to display it.

### Nettra RTU
[Nettra RTU](https://nettra.tech/en/how-we-do-it/rtu-x) called **"RTU-X"** is a powerful IoT electronic device that has digital and analog inputs and outputs, as well as several integrated communication interfaces as modem, ethernet, bluetooth, WiFi, RS485 and RS232. It is an ideal product to implement monitoring, data acquisition and control applications over a distributed data network.

The RTU-X is easly configurable via a [RTU-X Configuration Interface](http://wiki.nettra.tech/en/downloads). To adapt the RTU-X to each application, it runs a fully customizable script, accessible and editable from the Configuration Interface. In this guide we will provide one as an example quite simple and easy to understand.

Once you complete this sample/tutorial, you will see your sensor data on a dashboard like the following on the right.
<br><br>

<div align="center">

![rtu_x](/images/samples/nettrartu_x/rtu_x.png) ![dashboard](/images/samples/nettrartu_x/dash.png)

</div>


## Prerequisites <a name="prerequisites"></a>

This step shows what is necessary to accomplish this tutorial.

### Hardware

 - 1x RTU-X (you can get one [here](https://shop.nettra.tech/en/store/))
 - 1x 12VDC supply voltage

### Software
 - [RTU-X Configuration Interface](http://wiki.nettra.tech/en/downloads).
 - You will need to have ThingsBoard server up and running. Use either [Live Demo](https://thingsboard.io/docs/user-guide/install/installation-options/?ceInstallType=liveDemo) or [Installation Guide](https://thingsboard.io/docs/user-guide/install/installation-options/) to install ThingsBoard.

## Connection diagram <a name="connection_diagram"></a>

The following picture show the pinout of the RTU-X:
<br><br>
<div align="center">

![rtu_x_connections](/images/samples/nettrartu_x/rtu_x_connections.png)

</div>
<br>
Make sure to connect the positive rail of the supply to socket n°1 and its negative rail to socket n°3.
<br>

## ThingsBoard configuration <a name="tb_configuration"></a>
  
This step contains instructions that are necessary to connect your device to ThingsBoard.

Log in ThingsBoard Web UI as [Live Demo](https://demo.thingsboard.io/signup) or to your Thingsboard instance. See [ThingsBoard installation options](https://thingsboard.io/docs/user-guide/install/installation-options/) page for more details on how to get a Thingsboard instance running.

### Device

1. Go to *"Devices"* section. 
2. Click on *"+"* button and create a device with the name **"RTU-X"**. Set *"Device type"* to **"default"**.
<br><br>
<div align="center">

![add_device](/images/samples/nettrartu_x/add_device.png)

</div>
<br><br>
3. Once the device is created, open its details and click *"Copy access token"*. Please save this device token. It will be referred to later as **$TOKEN**.
<br><br>
<div align="center">


![dev_acc_tok](/images/samples/nettrartu_x/dev_acc_tok.png)

</div>

### Dashboard

Download the dashboard file (.json) using this [link](/docs/samples/nettrartu-x/resources/rtu_x_dashboard.json).
Use import/export [instructions](https://thingsboard.io/docs/user-guide/dashboards/#import-dashboard) to import the dashboard to your ThingsBoard instance.

## Connect RTU-X to PC <a name="connection_pc"></a>

 - Download and install the latest version of [RTU-X Configuration Interface](http://wiki.nettra.tech/en/downloads).
 - Turn on the RTU-X.
 - Check your wifi network and connect to "RTU-X-******".
 - Open the RTU-X Configuration Interface. 

   1. Go to *"Home"*.
   2. Click on *"TCP/IP"*.
   3. Specify the *"IP"* address **"192.168.4.1"**, *"Port":* **"502"** (by default).
   4. Click on *"Connect"*.

<div align="center">

   ![rtu_step1](/images/samples/nettrartu_x/rtu_step1.png)

</div>

 - Once you are connected you should see the following:

<div align="center">

   ![rtu_step2](/images/samples/nettrartu_x/rtu_step2.png)

</div>
  
 - Then:
   1. Go to *"Communications"*.
   2. Go to *"Wifi, Serial, Modbus"*.
   3. Check *"Station"* checkbox and fill in the credentials for the WiFi network.
   4. *"Apply Changes"*
   
<div align="center">

   ![rtu_step3](/images/samples/nettrartu_x/rtu_step3.png)

</div>
   
 - Finally:
   1. Go back to *"Home"*.
   2. Make sure the RTU-X has successfully connected to the WiFi network.

<div align="center">

   ![rtu_step4](/images/samples/nettrartu_x/rtu_step4.png)

</div>

## RTU-X configuration <a name="rtu_configuration"></a>

Once you have your RTU-X connected to the PC, we can proceed with its configuration.

### MQTT

1. Go to *"Communications"*.
2. Click on *"MQTT"*.
3. On *"Interface"* select *"Modem"*. On *"Format"* select *"Thingsboard"*. On *"URI"* paste *"mqtt://demo.thingsboard.io:1883"*. On *"Password"* paste the Device Acces Token from *"Device"* step.
4. Click on *"Apply Changes"*.

<div align="center">

![rtu_step5](/images/samples/nettrartu_x/rtu_step5.png)

</div>

### Script

1. Copy this [***script***](/docs/samples/nettrartu-x/resources/rtu_x_script.json).

```c
/*
 * DESCRIPTION :
 *	- Sending a variable to a Thingsboard Dashboard
 */
// VARIABLES DEFINITION ------------------------------------------
// User defined parameters
uint t_log = 10; // 'variable' log time in seconds

// Loggable variable
telemetry float variable = 0; // Parameter you want to visualize in Thingsboard
// 'variable' can be a BLE temperature measurement, a modbus preassure sensor value,
// a 4-20mA flowmeter value from the analog inputs and many more.

// SCRIPT -----------------------------------------------------------
while (1)
{
    variable = variable + 1; // variable is incremented by 1 in every loop
    log(variable);	
    delay(t_log * 1000); // 10 seconds
}
```
If you want to make your own script, you can see the [Nettra script user manual](http://wiki.nettra.tech/en/script).

2. Go to *"Script"*.
3. Paste the script. Compile and save the script in the RTU-X by clicking *"Compile & Apply"*.

<div align="center">

![rtu_step6](/images/samples/nettrartu_x/rtu_step6.png)

</div>

## Data visualization <a name="data_visualization"></a>

Finally, open ThingsBoard Web UI in the Live Demo server with same user and password as *ThingsBoard configuration* section.

Go to *"Devices"* section and locate *"RTU-X Device"*, open device details and switch to *"Latest telemetry"* tab.
If all is configured correctly you should be able to see latest values of *"variable"* in the table.<br><br>

<div align="center">

![last_telemetry](/images/samples/nettrartu_x/last_telemetry.png)

</div>

After, open *"Dashboards"* section then locate and open *"RTU-X"* dashboard.
As a result, you will see an analog gauge (similar to dashboard image in the introduction).<br><br>

<div align="center">

![dash](/images/samples/nettrartu_x/dash.png)

</div>

## See also

Browse other [samples](https://thingsboard.io/docs/samples/) or explore guides related to main ThingsBoard features:

 - [Device attributes](https://thingsboard.io/docs/user-guide/attributes/) - how to use device attributes.
 - [Data Visualization](https://thingsboard.io/docs/guides/#AnchorIDDataVisualization) - how to visualize collected data.
 - [Data Analytics](https://thingsboard.io/docs/guides/#AnchorIDDataAnalytics) - how to collect telemetry data.
 - [Rule Engine](https://thingsboard.io/docs/user-guide/rule-engine-2-0/re-getting-started/) - how to use rule engine to analyze data from devices.
 - [Using RPC capabilities](https://thingsboard.io/docs/user-guide/rule-engine-2-0/tutorials/rpc-request-tutorial/) - how to send commands to/from devices.

