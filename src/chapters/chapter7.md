## Analyze Big Data With Azure Data Warehouse and Power BI

In this chapter, you'll create an Azure SQL Data Warehouse, load the data from Azure Data Lake Store using PolyBase and analyze the data using Power BI.


### Azure SQL Data Warehouse
Azure SQL Data Warehouse is a cloud-based massively parallel processing (MPP) relational database, able to handle large enterprise workloads. Designed to efficiently scale up within minutes and integrate across the Azure platform. Azure SQL Data Warehouse compute can be paused and resumed on-demand to eliminate costs during non-business hours. The MPP architecture takes a divide and conquer approach against large distributed datasets. Storage and compute is decoupled allowing more flexibility to grow when required.


<h4 class="exercise-start">
    <b>Exercise:</b> Provision an Azure SQL Data Warehouse
</h4>

Browse to the following page https://portal.azure.com/ and log into your Azure account.

![Data Warehouse 002](images/chapter7/DWH002.png)

1. Click the + New to create a new Azure resource
2. Select *Databases*
3. Click on *SQL Data Warehouse*

An alternative is to search for *SQL Data Warehouse* in the Azure Marketplace. 

![Data Warehouse 001](images/chapter7/DWH001.png)

1. Click the + New to create a new Azure resource
2. Type *Data Warehouse* in the Search Box
3. Click on *SQL Data Warehouse* to create a new SQL Data Warehouse

Specify the properties of the New Data Warehouse. 

<img src="images/chapter7/DWH003.png" alt="Data Warehouse 003" class="img-small"/>

1. Specify name
2. Confirm the subscription 
3. Select the *Use existing* resource group
4. Select the previously created resource group
5. Select *Blank database* for the Select source
6. Click on the *Pin to dashboard* checkbox
7. Click on the *Create* button to provision the new data warehouse

Specify the server for the New Data Warehouse. 
![Data Warehouse 004](images/chapter7/DWH004.png)

1. Click *Server* to configure
2. Click *Create a new server*
3. Enter the Server Name
4. Enter a Server admin login
5. Enter a password (see guidelines below). Be sure to record the username and password -- you will need them later.
6. Confirm the password
7. Select the Location

> **NOTE:** Passwords must be at least 8 characters long and may not contain the account name of the user. In addition, passwords must contain characters from three of the following categories:
* Uppercase letters (A through Z)
* Lowercase letters (a through z)
* Digits (0 through 9)
* Special characters (e.g. !,$,#,%)


Specify the remaining server properties for the New Data Warehouse. 

<img src="images/chapter7/DWH005.png" alt="Data Warehouse 005" class="img-small"/>

1. Verify the correct server is selected
2. Leave the default Collation
3. Select 400 as the Performance level
5. Click the checkbox to Pin to Dashboard
6. Click *Create* to finish provisioning the data warehouse

This completes the exercise!
<div class="exercise-end"></div>

### Configure Application Access to the Azure Data Lake Store
Before we can access data from the Azure Data Lake Store using Azure SQL Data Warehouse, we will need to create and configure an Azure Active Directory application that will be authorized to have such access.

<h4 class="exercise-start">
    <b>Exercise:</b> Create and Configure Azure Active Directory Application
</h4>

In the Azure Portal, navigate to the Azure Active Director blade by typing in "Azure Active Directory" in the search bar at the top of the page. Then, select *Azure Active Directory* from the list of matching resources.

<img src="images/chapter7/ADLS Access/ADLS Access 1.png" class="img"/>

Click on *App registrations* in the navigation bar.

<img src="images/chapter7/ADLS Access/ADLS Access 3.png" class="img-small"/>

Click on * + New application registration*

<img src="images/chapter7/ADLS Access/ADLS Access 4.png" class="img"/>


Specify the details of the new application:

<img src="images/chapter7/ADLS Access/ADLS Access 5.png" class="img-small"/>

1. Provide the name for your application
2. Specify *Web app/API* as application type
3. Enter a URL in the Sign on URL field (this URL is not relevant for the purpose of this exercise -- you may specify any valid URL)
4. Click the *Create* button to create the App


Now that the application has been created, let us find and record several important attributes of the application that we will need in a subsequent exercises:
1. OAuth 2.0 Token Endpoint
2. Application Id 
3. Authentication Key

##### Find the OAuth 2.0 Token Endpoint
On the listing of registered apps, click on the *Endpoints* link.

<img src="images/chapter7/ADLS Access/ADLS Access 7.png" class="img"/>

On the following screen, you will see a list of endpoints associated with this Azure Active Directory APP. Scroll down to the *OAUTH 2.0 TOKEN ENDPOINT* area and click on the Copy icon to copy the endpoint URL to the clipboard.

<img src="images/chapter7/ADLS Access/ADLS Access 9.png" class="img-small"/>

Paste and save this URL in a text editor -- you will need it later.

##### Find Application Id
To find the Application Id of the application, navigate to the overview of the registered app, hover over the Application Id and click on the Copy icon that will appear.

<img src="images/chapter7/ADLS Access/ADLS Access 10.png" class="img"/>

Paste and save the Application Id in a text editor -- you will need it later.

##### Create the Authentication Key
Find the *Keys* link in the Settings blade for the Registered App. 

<img src="images/chapter7/ADLS Access/ADLS Access 11.png" class="img-small"/>

In the Keys blade, create and save a new Key:

<img src="images/chapter7/ADLS Access/ADLS Access 12.png" class="img"/>

1. Specify Key description
2. Set the expiration date
3. Click Save

When the authentication key is saved, a key value will be automatically generated. Copy this key, paste it to a text editor and save it -- you will need it later. 

<img src="images/chapter7/ADLS Access/ADLS Access 13.png" class="img"/>

>**NOTE:** The value of the key will not be visible after you leave the Keys blade - be sure to save it securely.

This completes the exercise!
<div class="exercise-end"></div>

### Grant Application Permissions to the Data Lake Store

Now, that the application has been created, let us grant it the necessary permissions to access the Azure Data Lake Store. 

<h4 class="exercise-start">
    <b>Exercise:</b> Grant Application Permissions to Data Lake Store
</h4>

In the Azure Portal, navigate to the Azure Data Lake Store blade by typing in "Data Lake Store" in the search bar at the top of the page. Then, select *Data Lake Store* from the list of matching resources.

<img src="images/chapter7/ADLS Access/ADLS Access 15.png" class="img"/>


Select the Data Lake Store that you had created earlier.

<img src="images/chapter7/ADLS Access/ADLS Access 16.png" class="img-medium"/>

In the Overview blade of the Data Lake Store, click on the Data Explorer link:

<img src="images/chapter7/ADLS Access/ADLS Access 17.png" class="img"/>

Select the root folder of your Azure Data Lake Store in the Data Explorer window.

<img src="images/chapter7/ADLS Access/ADLS Access 18.png" class="img-small"/>


Click on *Access* in the toolbar at the top of the screen.

<img src="images/chapter7/ADLS Access/ADLS Access 19.png" class="img"/>

In the Access blade, click on the *+ Add* button.

<img src="images/chapter7/ADLS Access/ADLS Access 20.png" class="img-medium"/>

Click on the *Select User or Group* link in the Assign Permissions blade.

<img src="images/chapter7/ADLS Access/ADLS Access 22.png" class="img-small"/>

Search for and select the Azure Active Directory application that you had registered earlier:

<img src="images/chapter7/ADLS Access/ADLS Access 23.png" class="img-small"/>

Click on the *Select Permissions* link in the Assign Permissions blade.

<img src="images/chapter7/ADLS Access/ADLS Access 24.png" class="img-small"/>

Specify the desired permissions:

<img src="images/chapter7/ADLS Access/ADLS Access 25.png" class="img-small"/>

1. Set Read and Execute permissions
2. Add the permissions to the selected folder and all child items
3. Add the permissions as an access permission entry and a default permission
4. Click *OK* to apply permissions.

Now, we can use the identity of the Azure Active Directory application that you had registered to view folder content and read files stored in the appropriate folder of the Azure Data Lake store.

This completes the exercise!
<div class="exercise-end"></div>

### Load Data into Azure SQL Data Warehouse using PolyBase

PolyBase is a technology that accesses data outside of the Azure SQL Data Warehouse via T-SQL. It is used to import/export data between Hadoop clusters, Azure Blob Storage, and Azure SQL Data Warehouse.

<h4 class="exercise-start">
    <b>Exercise:</b> Using PolyBase to connect to Azure Data Lake Store
</h4>

Open Azure SQL Data Warehouse and click on *Query editor (preview)* under Common Tasks.
![Data Warehouse 006](images/chapter7/DWH006.png)

The following message will appear describing the terms of the preview feature. Click the checkbox to accept the terms and then click *OK*.

<img src="images/chapter7/DWH007.png" alt="Data Warehouse 007" class="img-small"/>


Next, sign into the Azure SQL Data Warehouse using the Azure SQL Data Warehouse account from the previous exercise.
1. Click on the *Login* button
2. Select *SQL Server Authentication* in the Authorization Type field
3. Specify the user name that you had selected in a previous exercise
4. Specify the password that you had selected in a previous exercise
5. Click *OK* to complete the login process.

<img src="images/chapter7/DWH009.png" class="img-medium"/>


Once connected to the Azure SQL Data Warehouse, we can being writing queries directly in the browser. The following T-SQL script will create a Master Key and Credential to securely connect to Azure SQL Data Warehouse. 

> **NOTE:** This exercise uses Application Id, OAuth 2.0 Token Endpoint, and Authentication Key that you have obtained in a previous exercise in this chapter.

```sql
CREATE MASTER KEY;

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<application_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<authentication_key>'
;

-- The identity and secret should look similar to this example:
--    IDENTITY = '87815a3-4873-54fc-e8b1-789154591c0c2@https://login.microsoftonline.com/5b33523-95c5-61ac-a31b-7d0acd0ba8752/oauth2/token',
--    SECRET = 'GdeUjJsEJF7JdKFs+v5HSXyzOL+TkjzvNTxCsds3gWHN='
```

The next step is to create an external data source that points to the Azure Data Lake Store location, and accessed by using the credential created in the previous step.
```sql
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    --For example: 'adl://myazurelakestorename.azuredatalakestore.net'
    CREDENTIAL = ADLCredential
);

```

Next, we need to define the external file format for the PolyBase engine to process the data.
```sql
CREATE EXTERNAL FILE FORMAT DeviceTelemetryDelimitedText
WITH (
    FORMAT_TYPE = DELIMITEDTEXT
    ,FORMAT_OPTIONS
    (FIELD_TERMINATOR = ','
     ,STRING_DELIMITER = ''
     ,DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fff'
     ,USE_TYPE_DEFAULT = FALSE
    )
);
```

Now that the credential, data source, and file format have been created, we are ready to define the external table. When a T-SQL query referencing this external table is executed, the PolyBase engine will push down the call to the underlying file system.

```sql
CREATE EXTERNAL TABLE dbo.DeviceTelemetryExternal (
    [DeviceId] [varchar](100) NULL,
    [DateTime] [varchar](100) NULL,
    [TempC] [numeric] NULL,
	[RunTime] [int] NULL
)
WITH (
    LOCATION='/device-operating-data/'
    , DATA_SOURCE = AzureDataLakeStore
    , FILE_FORMAT = DeviceTelemetryDelimitedText
    ,REJECT_TYPE = VALUE
    ,REJECT_VALUE = 100
);
```

Let us verify that we are able to read the data from the newly created external table by executing a simple SELECT statement:

```sql
SELECT TOP 100 *
FROM dbo.DeviceTelemetryExternal
```

While the PolyBase engine allows ad-hoc queries involving external tables, the best practice is to load external data into the native tables in the Azure SQL Data Warehouse. The next step will load external data from the Data Lake Store into Azure SQL Data Warehouse. We will use the Create Table as Select (CTAS) construct  which is a parallelized operation that efficiently creates a table from a large dataset. When defining the query, the distribution can be defined that splits up the data across multiple nodes of the data warehouse. In the script below, the hash of the DeviceId column was selected to split the data across the storage nodes.

```sql
CREATE TABLE dbo.DeviceTelemetry  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH(DeviceId))  
AS  
SELECT 
    CAST([DeviceId] AS [varchar](100)) AS DeviceId,  
    CAST([DateTime] AS DATETIME2) AS DateTime,  
    CAST([TempC] AS [numeric]) AS TempC,  
    CAST([RunTime] AS [int]) AS RunTime
FROM dbo.DeviceTelemetryExternal

CREATE STATISTICS DeviceTelemetryDeviceIdStats on dbo.DeviceTelemetry(DeviceId);
```
Now, let's create an external table and load reference data describing each of the devices.

```sql
CREATE EXTERNAL TABLE dbo.DeviceReferenceExternal (
    [Device Id] [varchar](100) NULL,
    [Motor Type] [varchar](100) NULL,
    [Device Type] [varchar](100) NULL,
    [Max Operating Temperature] numeric NULL,
    [Production Date] [varchar](100) NULL,
    [Overhaul Date] [varchar](100) NULL,
    [Overhaul Run Time] int NULL,
    [Maintenance Date] [varchar](100) NULL,
    [Maintenance Run Time] int NULL
)
WITH (
    LOCATION='/device-operating-data/DeviceReferenceData.csv'
    , DATA_SOURCE = AzureDataLakeStore
    , FILE_FORMAT = DeviceTelemetryDelimitedText
    ,REJECT_TYPE = VALUE
    ,REJECT_VALUE = 100
);
```

Then, let's create a local table with device reference data. You will notice that this table with reference data is being distributed across storage nodes of the data warehouse in a manner similar to the distribution of the device telemetry data to help optimize join performance.

```sql
CREATE TABLE dbo.DeviceReference  
WITH (DISTRIBUTION = HASH(DeviceId))  
AS  
SELECT 
    [Device Id] AS DeviceId,
    [Motor Type] AS MotorType,
    [Device Type] AS DeviceType,
    ([Max Operating Temperature] - 32)/1.8 AS MaxOperatingTemperatureC,
    CAST([Production Date] AS date) AS ProductionDate,
    CAST([Overhaul Date] AS date) AS OverhaulDate,
    [Overhaul Run Time] AS OverhaulRunTime,
    CAST([Maintenance Date] as date) AS MaintenanceDate,
    [Maintenance Run Time] AS MaintenanceRunTime
FROM dbo.DeviceReferenceExternal

CREATE STATISTICS DeviceReferenceDeviceIdStats ON dbo.DeviceReference (DeviceId);
```



Finally, we will execute a query that will allow us to join telemetry data with reference data and retrieve the average, minimum and maximum temperatures, as well as the count of records for each combination of device type and motor type.

```sql
SELECT R.DeviceType,
    R.MotorType,
    COUNT(DISTINCT T.DeviceId) AS DistinctDevices,
    COUNT(*) AS Observations,
    AVG(T.TempC) AS AverageTemperatureC,
	MIN(T.TempC) AS MinimumTemperatureC,
	MAX(T.TempC) AS MaximumTemperatureC,
    CAST(COUNT(CASE WHEN T.TempC > R.MaxOperatingTemperatureC THEN 1 END) AS numeric)/COUNT(*) 
        AS [ExcessiveTemperature%]
FROM dbo.DeviceTelemetry T
    JOIN dbo.DeviceReference R 
        ON T.DeviceId = R.DeviceId
GROUP BY R.DeviceType,
    R.MotorType
ORDER BY R.DeviceType,
    R.MotorType
```

This completes the exercise!
 
<div class="exercise-end"></div>

<br/>

### Visualize data using Power BI

<h4 class="exercise-start">
    <b>Exercise:</b> Connecting Azure SQL Data Warehouse to Power BI
</h4>

Open Azure SQL Data Warehouse and click on Open in Power BI under Common Tasks. 

<img src="images/chapter7/DWH010.png" class="img"/>

You may be asked to enter your username and password to log into the Power BI service.

>**Note:** Your credentials to the Power BI account may or may not be the same as your credentials to your Azure subscription.

During the next step, you will confirm the names of the Azure SQL Server and Database. Click Next to continue.

<img src="images/chapter7/PowerBI 1.png" class="img-large"/>

Enter the username and password for the Azure SQL Data Warehouse account that you had created earlier. Then press the *Sign In* button to connect to the Azure SQL Data Warehouse. 

<img src="images/chapter7/DWH012.png" class="img-medium"/>

A new Power BI dataset connected to Azure SQL Data Warehouse will be created.

You will see a new report canvas that you will use to create a new report. 

Start by creating a bar chart that summarizes average temperatures by device. 

<img src="images/chapter7/PowerBI 3.png" class="img-large"/>

1. Select the bar chart visual from the visualizations pallette
2. Drag and drop the bar chart visual to the report canvas and expand it to a larger size.
3. Select DeviceId field from the DeviceTelemetry table
4. Drag and drop the DeviceId field to the Axis placeholder
5. Select TempC field from the DeviceTelemetry table
6. Drag and drop the TempC field to the Value placeholder
7. Click on the downward-pointing arrow in the Value placeholder
8. Select *Average* from the pop-up menu.

Now, let us enhance this chart by representing not only the average temperature, but also the volatility of temperatures for each device.
<img src="images/chapter7/PowerBI 4.png" class="img-large"/>

1. Select TempC field from the DeviceTelemetry table
2. Drag and drop the TempC field to the Color saturation placeholder\
3. Click on the downward-pointing arrow in the Color saturation placeholder
4. Select *Standard deviation* from the pop-up menu.

This completes the exercise!

<div class="exercise-end"></div>

<br/>

### Workshop Completed
Congratulations! You have successfully completed the workshop and have built an end-to-end real-time predictive maintenance solution using Azure Machine learning, IoT Hubs, Stream Analytics, and Power BI