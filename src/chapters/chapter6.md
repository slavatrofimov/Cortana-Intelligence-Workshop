## Use Azure Data Factory to Load Data into Data Lake Store

In this chapter, you'll learn how to create an Azure Data Factory pipeline and copy data from Azure Blob Storage to Azure Data Lake store. 

### Create Azure Data Factory
Azure Data Factory is a cloud-based integration service for orchestrating data movements and data transformations. These operations are called pipelines and can be schedule to ingest data from multiple sources, process data using compute services (Azure HDInsight, Hadoop, Spark, Azure Data Lake Analytics, Azure Machine Learning, etc.), and publish to data stores such as Azure Data Lake Store.

<h4 class="exercise-start">
    <b>Exercise 1</b>: Provision a Data Factory
</h4>

Browse to the following page https://portal.azure.com/ and log into your Azure account. 

![Data Factory 001](/images/chapter6/DF_001.png)
1. Click the New + to create a new Azure Resource
2. Select Data + Analytics 
3. Click on Data Factory

An alternative is to search for Data Factory in the Azure Marketplace.
![Data Factory 002](/images/chapter6/DF_002.png)
1. Click the New + to create a new Azure Resource
2. Type Data Factory in the Search Box
3. Click on Data Factory

On the next blade menu click on the *Create* button to provision the Azure Data Factory.

![Data Factory 003](/images/chapter6/DF_003.png)

Specify the properties of the New data factory.

<img src="images/chapter6/DF_004.png" class="img-medium" />

1. Specify name
2. Confirm the subscription 
3. Select the use existing resource group
4. Select the previous resource group
5. Select the desired location
6. Click on the *Pin to dashboard* checkbox
7. Click on the *Create* button to provision the data factory

This completes the exercise!
<div class="exercise-end"></div>

<br/>

### Complete Azure Data Factory Copy Wizard

<h4 class="exercise-start">
    <b>Exercise 2 :</b> Copy Files using Azure Data Factory Copy Wizard
</h4>

<b>2.1</b> - Once the data factory has been created, open the resource and click on *Copy data (PREVIEW)*. This will open a new tab to the Azure Data Factory Copy Wizard. 

![Data Factory 005](/images/chapter6/DF_005.png)

<b>2.2</b> - On the Properties menu of Copy Data complete the following tasks.

![Data Factory 006](/images/chapter6/DF_006.png)
1. Specify a task name
2. Enter a task description 
3. Select Run once now
4. Click on the *Next* button

<b>2.3</b> - On the Source Connection select Azure Blob Storage from the list. Click the *Next* button to continue. 

![Data Factory 007](/images/chapter6/DF_007.png)


<b>2.4</b> On the following screen, enter the storage account information. Click the *Next* button to continue.

<img src="images/chapter6/DF_008.png" class="img-medium" />
1. Specify a connection name
2. Select Enter manually from the Account selection method
3. Enter the storage account name: *kizandevices*
4. Enter the storage account key 
**Your storage account key will be provided during the workshop**
5. Click on the *Next* button

<b>2.5</b> On the following screen, select the input folder *device-operating-data*. Then, click the *Choose* button.

![Data Factory 009](/images/chapter6/DF_009.png)

<b>2.6</b> On the following screen, click the check box for copying files recursively. Click the *Next* button to continue.

![Data Factory 010](/images/chapter6/DF_010.png)

<b>2.7 A</b> - Azure Data Factory will then scan the files selected and automatically detect the File Format settings.

<img src="images/chapter6/DF_011.png" class="img-medium" />

<b>2.7 B</b> - In addition to the settings, a preview of the files will be shown. Once all settings are correct, click the *Next* button.

<img src="images/chapter6/DF_012.png" class="img" />

<b>2.8</b> - On the Destination data store screen, select Azure Data Lake Store from the list. Click the *Next* button to continue. 

![Data Factory 013](/images/chapter6/DF_013.png)

<b>2.9</b> - Next we will enter the Azure Data Lake Store connection details. 

<img src="images/chapter6/DF_014.png" class="img-medium" />
1. Specify a connection name
2. Select *From Azure subscriptions* as the Data Lake selection method
3. Select the Azure subscription 
4. Select the Data Lake store account name
5. Select the Authentication type as OAuth (This will prompt for account information on a later step)
6. Click on the *Next* button

<b>2.10</b> The next step is to control how the data will be copied. The options available are the following.

* Merge files - will combine files into one large file
* Preserve hierarchy - copy all files and folder structures
* Flatten hierarchy - remove all folders and copy all files into one folder

Select *Preserve hierarchy* and click the *Next* button to continue. 

![Data Factory 015](/images/chapter6/DF_015.png)

<b>2.10</b> The next step is to control how the data gets saved. Make sure the *Add header to file* checkbox is checked. Click the *Next* button to continue.

<img src="images/chapter6/DF_016.png" class="img-medium" />


<b>2.11</b> Settings will control how the data is moved in Azure. These settings can be changed to allocate a specific number of resources to copy data. Leaving these at Auto will let Azure determine the proper number of resources. Click the *Next* button to continue.

<img src="images/chapter6/DF_017.png" class="img-medium" />

<b>2.12</b> - The summary screen contains a detail list of the options selected for the Copy Wizard. Click the *Authorize* button to enter account information required on step 2.9. Click the *Next* button to continue.

![Data Factory 018](/images/chapter6/DF_018.png)

<b>2.13</b> - A popup window will prompt for Azure account information. Sign in to continue.

<img src="images/chapter6/DF_019.png" class="img-medium" />

<b>2.14</b> - Review the Summary page. Once approved, click the *Next* button to begin the deployment process of the Azure Data Factory.

![Data Factory 020](/images/chapter6/DF_020.png)

<b>2.15</b> - Once deployment is complete, follow the *Click here to monitor copy pipeline* link.

![Data Factory 021](/images/chapter6/DF_021.png)

<b>2.16</b> - The Azure Data Factory Resource Explorer will be displayed. In the lower middle section, under ACTIVITY WINDOWS, the currently deployed pipeline will be displayed. Monitor the duration to see how long the copy process will take to complete.

![Data Factory 022](/images/chapter6/DF_022.png)

This completes the exercise!

<div class="exercise-end"></div>
