## Provision Azure IoT Hub and Azure Data Lake Store

The architecture of most IoT solutions includes several common components, such as a hub that receives messages from connected devices and a big data store that could be used to permanently store the data collected from the devices. We will create both of these resources during this section of the workshop.

### Create an Azure IoT Hub
Let us create an Azure IoT Hub to serve as a central ingestion point for telemetry data sent by our connected devices. Azure IoT Hub supports billions of clients that can securely send data to the hub to report on their state and operating conditions. Azure IoT Hub supports bi-directional communications by allowing cloud-to-device messages to be sent to the devices.

<h4 class="exercise-start">
    <b>Exercise</b>: Create an Azure IoT Hub
</h4>

Log into your Azure Portal by navigating to https://portal.azure.com.

Click on the "+" sign in the upper left corner and type in the term "IoT Hub" in the Search bar, then select "IoT Hub" from the list of matching resource types.

<img src="images/chapter3/IoT Hub/IoT Hub 1.png" class="img-medium" />

Review the name of the resource and click on the *Create* button.

<img src="images/chapter3/IoT Hub/IoT Hub 2.png" class="img-medium" />

Specify the parameters of the IoT Hub:

>**NOTE:** The name of the IoT Hub must be globally unique across all Azure subscriptions. If the name you tried to use is not available, please specify a different name.

1. Specify the name of the hub
2. Select pricing tier: F1-Free
3. Select Azure Subscription in which the hub will be created
4. Indicate that you will be using an existing resource group
5. Select resource group name
6. Specify the location for the IoT Hub
7. Press the *Create* button

<img src="images/chapter3/IoT Hub/IoT Hub 3.png" class="img-medium" />

Once the IoT Hub has been created, take a few moments to review the IoT Hub blade in your Azure Portal and familiarize yourself with the features and parameters of the IoT Hub.

> **NOTE:** Provisioning of an IoT Hub is a key part of building an real-time analytics solution for connected devices. During this workshop, we will be using an IoT Hub provisioned by KiZAN. Therefore, the IoT Hub that you had just provisioned will be present in your subscription, but will not be actively used throughout the remainder of the workshop.

<div class="exercise-end"></div>

### Create an Azure Data Lake Store
Let us create a data lake store to store to store the telemetry data from our IoT devices. Azure Data Lake Store is a secure, massively-scalable big data storage service for unstructured, semi-structured, and structured data. Azure Data Lake Store can store trillions of files with individual files being over a petabyte in size, which makes it ideal for a variety of enterprise and scientific applications. The Data Lake Store can be used to capture data of any size, type and velocity to support operational and exploratory analytics.

<h4 class="exercise-start">
    <b>Exercise</b>: Create an Azure Data Lake Store
</h4>

Log into your Azure Portal by navigating to https://portal.azure.com.

Click on the "+" sign in the upper left corner and type in the term "Data Lake" in the Search bar, then select "Data Lake Store" from the list of matching resource types.

<img src="images/chapter3/Data Lake Store/DataLakeStore 2.png" class="img-medium" />

Review the name of the resource and click on the *Create* button.

<img src="images/chapter3/Data Lake Store/DataLakeStore 3.png" class="img-medium" />

Specify the parameters of the Data Lake Store:

>**NOTE:** The name of the data lake store must be globally unique across all Azure subscriptions. If the name you intended to use is not available, please specify a different name.

1. Specify the name of the Data Lake Store
2. Subscription
3. Indicate that you will be using an existing resource group
4. Select resource group name
5. Specify location: *East US 2*
6. Select pricing tier
7. Enable encryption to secure your data at rest
8. Check the box to pin the resource to your dashboard in the Azure Portal
9. Press the *Create* button

<img src="images/chapter3/Data Lake Store/DataLakeStore 4.png" class="img-medium" />

>**NOTE:** It is typically a good practice to provision related data-intensive resources in the same location - this will help to minimize latency and maximize throughput while one service accesses resources stored in another service. This approach also helps to minimize egress charges (charges for data leaving an Azure data center or data being moved from one data center to another data center). While not every resource type is available in every Azure location, we will plan to provision most of the resources in the East US 2 Azure location during this workshop.

<div class="exercise-end"></div>

