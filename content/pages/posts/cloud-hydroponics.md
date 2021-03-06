---
title: Cloud Hydroponics
excerpt: >-
  Cloud hydroponics is a prototype azure eventhub and raspberry pi driven
  sensoring system used to monitor greenhouse hydraulic systems. Alerts and
  control limits work together to surface pump failure conditions and
  atmospheric deviations.
date: '2020-03-10'
thumb_img_path: /images/Hydroponics.jpg
thumb_img_alt: Hikers on the trail
content_img_alt: Hikers on the trail
layout: post
---
###

![Pi_Computer](https://user-images.githubusercontent.com/84352976/120264534-dc0edb00-c252-11eb-96ed-9834a28466bf.jpg)

In the current hydroponics industry, sensors are used to monitor greenhouse floor-level hydraulic systems to monitor for both water and air deviations in atmospheric conditions. The downtime of any components in this sensoring setup would cause significant damage to greenhouse plant health. Cloud Hydroponics is a cloud azure instrumentation system to complement the existing floor level greenhouse networks. Cloud instrumentation will allow alerting, monitoring, and real time storage of sensor telemetry at scale with customizability.

The system architecture is describled in Figure 1. A floor level master computer is used to control the pis while the pis upload telemetry events to the azure event-hub. (https://azure.microsoft.com/en-us/services/event-hubs/). Telemetry events are ingested and built into a stream with azure data lake storage and processed for Email and Text Alerting. Control-Charts, Rule based Alerting, and Historical Analysis is then built on the azure data lake layer. (https://azure.microsoft.com/en-us/solutions/data-lake/)

Github: https://github.com/OptimChain/Cloud_Hydroponics

Figure 1: Cloud Azure Architecture

![Home Pic](https://user-images.githubusercontent.com/84352976/120264166-12982600-c252-11eb-9d1c-c00834064945.png)

### To set up the pi system:

Pi Setup:

1.  Fork the code within the Hydroponics_Driver folder:
2.  Install Orchestrator.py as a python module within the Raspbian OS. To use the Raspbian OS, see: https://www.raspberrypi.org/software/
3.  Run Orchestrator.py within the master computer to send GPIO signals within GPIO 2. The flow sensor should be connected to GPIO 2 with group and 5v connected to the relevent pins: https://www.raspberrypi.org/documentation/usage/gpio/
4.  To onboard additional Pis, loop additional functions in the iothub_client_telemetry_sample_run() function or build additional DeviceIds to onboard in more raspberry pis.

Simulated Telemetry Setup:

1.  Fork the code within the Hydroponics_Driver folder:
2.  Install Simulated_Telemetry.py within any local computer python program. When this is run, simulated pulse telemetry will flow into our system

### To view the Cloud System:

1.  Log into the Azure Portal: https://azure.microsoft.com/en-us/features/azure-portal/

*   Login: cloud@optimchain.org
*   Pass: Contact cloud@optimchain.org

2.  The hydrostor account contains the root for stored telemetry:

![image](https://user-images.githubusercontent.com/84352976/119286880-30cea800-bbfa-11eb-99b6-5a16a6eaa7b5.png)

3.  The flowdatacontainer account contains all archived telemetry :

![image](https://user-images.githubusercontent.com/84352976/119287003-712e2600-bbfa-11eb-80d0-5f72538eb08f.png)

![image](https://user-images.githubusercontent.com/84352976/119287091-9de23d80-bbfa-11eb-93f1-5ba6eaa8084e.png)

### To configure the eventhub

The HydroIoTHub eventhub  contains all sent events. Go here to configure new Pi devices or change the connection string for devices. The current connection string for the first device is located within the github repo.

![image](https://user-images.githubusercontent.com/84352976/119287167-c702ce00-bbfa-11eb-8de0-47991c9f576a.png)

Comm-serv contains all the emails and text alerting services

![image](https://user-images.githubusercontent.com/84352976/119289087-c5d3a000-bbfe-11eb-93c4-2459a40b9d6c.png)

### To setup the Dashboarding System:

1.  Fork the code inside the Hydroponics_Dashboard folder
2.  Run app.py to build a local version of the dashboard (Figure 5)
3.  If any events arrive at the event-hub, then these datapoints will show up in this dashboard
