* TOC
{:toc}


## What is ThingsBoard Edge?

ThingsBoard Edge is a ThingsBoard's software product for edge computing. 
It allows bringing data analysis and management to the edge, where the data created. At the same time ThingsBoard Edge seamlessly synchronizing with the ThingsBoard cloud (ThingsBoard Cloud, ThingsBoard Demo, ThingsBoard PE or ThingsBoard CE) according to your business needs.
If this is your first experience with the edge we recommend to review [what-is-edge](/docs/{{docsPrefix}}edge/getting-started-guides/what-is-edge/) 
and [getting started guide](/docs/{{docsPrefix}}edge/getting-started/).
You can find more information on the dedicated page.

## How do I get started?

We recommend to [install](/docs/user-guide/install/{{docsPrefix}}edge/installation-options/) ThingsBoard Edge locally on your laptop or PC using Docker
and follow the [getting started guide](/docs/{{docsPrefix}}edge/getting-started/).

## Can multiple tenants or customers access single ThingsBoard Edge on remote location?

ThingsBoard Edge is **single** Tenant and **single** Customer entity.
You cannot share ThingsBoard Edge between multiple tenants or customers. 
In this case you'll need to provision multiple ThingsBoard Edge instances for every tenant (customer).
But you can use a single ThingsBoard Edge instance for one tenant and one customer from the same tenant.  

## Can I connect devices from multiple tenants to a single ThingsBoard Edge?

ThingsBoard Edge is **single** Tenant.
You cannot connect devices from multiple tenants to a single ThingsBoard Edge entity. 
In this case you'll need to provision multiple ThingsBoard Edge instances for every tenant.

## What can I do with ThingsBoard Edge?

With ThingsBoard Edge, you can connect your on-site devices to ThingsBoard Edge, that is installed on-site as well, instead of direct connection to ThingsBoard cloud and get next benefits:
- **Local deployment and storage**<br>
*Process and store data from edge (local) devices without connection to the cloud. Push updates to the cloud once connection restored.*
- **Traffic filtering**<br>
*Filter data from edge (local) devices on the ThingsBoard Edge service and push to cloud only subset of the data for further processing or storage.*
- **Local alarms**<br>
*React instantly to critical situations on site without connectivity to cloud.*
- **Batch update and visualization**<br>
*Update thousands of edge configurations in a single click. Monitor local events and timeseries data with a real-time dashboard.*

## How to connect my device?

ThingsBoard provides
[MQTT](/docs/{{docsPrefix}}edge/reference/mqtt-api), 
[CoAP](/docs/{{docsPrefix}}edge/reference/coap-api), 
[HTTP](/docs/{{docsPrefix}}edge/reference/http-api), and
[LwM2M](/docs/{{docsPrefix}}edge/reference/lwm2m-api) protocols support.
**Existing** devices may be connected to the platform using **[ThingsBoard Gateway](/docs/iot-gateway/what-is-iot-gateway/)**.
You can find more information on the [connectivity](/docs/{{docsPrefix}}edge/reference/protocols/) page. 

## Do I need to use an SDK?

No, many IoT devices can't afford to embed third-party SDK. ThingsBoard Edge provides quite simple API over common IoT protocols. You can choose any client-side library you like or use your own.
Some useful references:
 
 - [MQTT client-side libraries list](https://github.com/mqtt/mqtt.github.io/wiki/libraries) 
 - [C-implementation for CoAP](https://libcoap.net/)

## What about security?

You can use MQTT (over SSL) or HTTPS protocols for transport encryption. 

Each device has unique access token credentials that is used to setup connection. Credentials type is pluggable, so X.509 certificates support is coming soon.

## How many devices can ThingsBoard Edge support?

Number of connected devices depends on the hardware that is used for ThingsBoard Edge.
{% if docsPrefix == 'pe/' %}
Default licensing model doesn't allow to connect more than 1000 devices to a single ThingsBoard Edge. 
If your use case requires more, please [Contact us](/docs/contact-us/) so we can provide a solution for your use case.
{% else %}
ThingsBoard Edge designed in mind as an edge computing service, located in remote locations with possible low bandwidth connectivity, so we do not recommend connecting more than 1000 devices to a single edge.
{% endif %}
  
## Where does ThingsBoard Edge store data?

The data is stored in [PostgreSQL](https://www.postgresql.org/) database. PostgreSQL suites well for storage and querying of entities and local time-series data.
 
## How to get support?

You can use troubleshooting instructions and community resources or [contact us](/docs/contact-us) and learn more about [services](/docs/services/) we provide.