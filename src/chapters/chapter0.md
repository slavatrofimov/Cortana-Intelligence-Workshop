## Introduction

Welcome to the Real-Time Predictive Maintenance Solution with Cortana Intelligence Workshop!

### About the Workshop
Build an end-to-end real-time predictive maintenance solution using Azure Machine learning, IoT Hubs, Stream Analytics, and Power BI. In this workshop you'll also learn how to store and manipulate massive amounts of data using Azure Data Lake Store and Azure Data Warehouse. The workshop is heavily focused on:
* Machine Learning
* Real-Time Analytics 
* Big Data Analytics

The workshop is presented by:
* Slava Trofimov [KiZAN Technologies](http://kizan.com)
* Lucas Feiock [KiZAN Technologies](http://kizan.com)
* Mike Branstein [KiZAN Technologies](http://kizan.com)

### Solution Architecture
The architecture of the  predictive maintenance solution built during this workshop is shown on the following diagram:

<img src="images/chapter0/Predictive Maintenance Solution Architecture.png" class="img-large" />


### Agenda
#### Machine Learning
* Provision a resource group for the experiment
* Provision a machine learning workspace, 
* Build a machine learning model to predict remaining useful life of a device, and publish as a web service
	
#### Real-Time Analytics
* Provision Data Lake Store
* Provision, configure and start a Stream Analytics job
* Invoke a machine learning function to predict remaining useful life
* Build a Power BI report and dashboard to visualize streaming data

#### Big Data
* Provision Azure Data Factory; create and execute a job to copy additional data from KiZAN's blob storage to Azure Data Lake Store
* Provision an Azure SQL Data Warehouse
* Register an Application with Azure Active Directory and grant permissions to the Azure Data Lake Store
* Load data from Azure Data Lake Store to Azure SQL Data Warehouse
* Query Azure SQL Data Warehouse
* Connect to Azure SQL Data Warehouse using Power BI and create a report

### Prerequisites
* **Computer** with a modern Web browser and internet access (the computer may run any operating system and does not require any special software besides the web browser)
* **Access to a Microsoft Azure subscription** with permissions to create resource groups and other resources 
* **Access to a Power BI account** (either a free or a Pro account)

