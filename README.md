# HoloLensApp
A mixed reality application using Azure Cloud and Microsoft Hololens using Digital Twins

## Aims
As part of my Year In Industry, I led training to engineers to use the Microsoft HoloLens so that virtual
inspections could be conducted without travelling- especially crucial during the Covid-19 pandemic.
This barely grafts the capabilities of said device, and I feel like there is untapped potential in the ways
that we could use the HoloLens; hence I want to develop an application that will help the engineers.

One way to achieve helping engineers is to provide tools to help them diagnose faults and see the
current status, which could be achieved by displaying live data from the sensors on the HoloLens. This
will provide engineers with relevant information in their field of view, rather than holding a separate
device, which will increase productivity.

## Architecture
![image](https://github.com/themegaphoenix/HoloLensApp/assets/9766462/d4d2b661-e97d-4517-a2e9-5637e15b4a1d)

As this is an IoT application, the data flow is essential to the solution. Based on my literature review, I have designed an architecture that is scalable and can be implemented within the budget constraints:

 The Architecture of the data flow can be broken into three components:
•	The Raspberry PI –uses sensors such as a thermometer to measure the temperature
•	The Azure Cloud –is responsible for receiving, process, storing and broadcasting the data
•	The HoloLens app- receives the data and uses it to display the data

### Raspberry PI
This device will retrieve the data from the sensors and send it to the cloud. A data simulator with a Python script that sends data to the IoT cloud will be used for development. It can also be replaced by any other service that can send data to the cloud. 

### Azure Cloud
I have tried to use as many serverless services as possible as it allows me to scale when multiple sensors are introduced, as it is not tied to the specification of a machine. This will mean that the architecture can achieve the requirement to scale to thousands of devices.
#####	IoT Hub
This is where the data collected from the Raspberry PI will be sent to. It is essentially a message broker that is suited to IoT messages and devices. As it is a message broker, I can redirect the messages to the relevant services.
#####		Azure Digital Twins
Based on my research, Azure Digital twins allow us to represent objects digitally. Although it would be simpler to bypass this and store the values in a database and retrieve the latest readings, modelling the power station opens up more options for future versions. We could run machine learning to predict faults before it happens and infer where the fault could lie, i.e. related joined components.
#####		Azure Event Grid
One of the requirements is to be able to scale. Azure Event grid would allow us to fire off an action every time there is new data. Thus it makes it scalable as it is not dependent on the server specifications to run and can increase automatically when the load increase. This makes an event-driven architecture.
#####		Azure SignalR
SignalR would allow broadcasting the data to all the clients connected. This is a better method, as the device does not have to poll for new data, so there will be a lower delay retrieving the live data and lower service usage. This is because the Signal IR broadcasts it continuously rather than a device making continuous API calls to refresh the data. An analogy to this method is that satellite TV is distributed, the satellite broadcasts it and the satellite box decode, compared to network streaming, where the device asks the server to send the data.
####	Microsoft HoloLens Application
For the application that will be developed, I decided to go for a Unity 3D application. This is mainly due to the documentation that Microsoft provides being catered for it. The Mixed Reality Toolkit that provides UI components for the HoloLens is also developed for Unity. This application will subscribe to the Azure SignalR broadcast allowing it to display live data to the user into dashboards. These dashboards will be fixed onto a location using Azure Spatial Anchors.


## Disertation
Please see [Dissertation](Dissertation.pdf) or [Presentation](Presentation.pptx) for more information.

## Demo

https://github.com/themegaphoenix/HoloLensApp/assets/9766462/f02d86fe-8cc0-40a5-8972-a9c4128235b5

https://github.com/themegaphoenix/HoloLensApp/assets/9766462/8892e006-4911-4c7a-aa69-8db3b6335154

https://github.com/themegaphoenix/HoloLensApp/assets/9766462/431421a5-3c6d-4d0b-bd2e-e0149ef82ede

## Source Code
As this was an application developed under Uniper sponsorship, the source code is not available publically.




