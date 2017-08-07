## Create an Azure Stream Analytics Job

Once telemetry data from our connected devices has been ingested, we can use use Azure Stream Analytics to perform real-time processing and analysis of massive volumes of data in motion. Azure Stream Analytics supports connectivity to event streams (such as IoT Hubs and Event Hubs), as well as to reference data that changes infrequently. Azure Stream Analytics transformations are defined using a simple SQL-like language that has been extended to support the temporal (time-based) nature of the data. Azure Stream Analytics is capable of processing complex events in a variety of formats.

### Create and Configure the Job
<h4 class="exercise-start">
    <b>Exercise</b>: Create an Azure Stream Analytics Job
</h4>

Log into your Azure Portal by navigating to https://portal.azure.com.

Click on the "+" sign in the upper left corner and type in the term "IoT Hub" in the Search bar, then select "IoT Hub" from the list of matching resource types.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 1.png" class="img-medium" />

Review the name of the resource and click on the *Create* button.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 2.png" class="img-medium" />

Specify the parameters of the Stream Analytics Job:

1. Specify the name of the job
2. Select Azure Subscription in which the job will be created
3. Indicate that you will be using an existing resource group
4. Select resource group name
5. Specify the location for the IoT Hub
6. Check the box to pin the resource to your dashboard in the Azure Portal
7. Press the *Create* button

<img src="images/chapter4/Stream Analytics/StreamAnalytics 3.png" class="img-medium" />

Once the Stream Analytics job has been created, take a few moments to review the Stream Analytics blade in your Azure Portal and familiarize yourself with the features and parameters of this resource.

<div class="exercise-end"></div>

### Configure Inputs for the Stream Analytics Job
A stream analytics job must have one or more input and one or more output. Our job will have two inputs and two outputs. Let's start by creating our first input.

<h4 class="exercise-start">
    <b>Exercise</b>: Configure Inputs
</h4>

> **NOTE:** Names and configuration settings described in this exercise must match those listed in the instructions.


#### Create the Data Stream Input

Navigate to the *Overview* blade of your Stream Analytics job and click on the *Inputs* tile.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 4.png" class="img" />

Click on the *Add* button to add your first input.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 5.png" class="img-medium" />

Define the details for the input:

1. Specify the name or the alias for the input: *KiZAN-IoT-Hub*
2. Set Source Type to *Data stream*
3. Set Source to *IoT Hub*
4. Set import option to *Provide IoT hub settings manually*
5. Set IoT hub to *IOTH-KiZANCortanaWS01*
6. Set endpoint to *Messaging*
7. Set shared access policy name to *device*
8. Shared access policy key: **Your shared access policy key will be provided during the workshop**
9. Consumer group: **Your consumer group name will be provided to you during the workshop**
10. Set event serialization format to *JSON*
11. Set Encoding to *UTF-8*
12. Press the *Create* button

<img src="images/chapter4/Stream Analytics/StreamAnalytics 6.png" class="img-medium" />

#### Create the Reference Data Input

In addition to the streaming events, a Stream Analytics Job may utilize reference data, such as device metadata or other types of data that do not change frequently. We will join device metadata with reference data in order to enrich the outputs of the Stream Analytics Job.

Navigate to the *Overview* blade of your Stream Analytics job and click on the *Inputs* tile.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 7.png" class="img" />

Click on the *Add* button to add your second input.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 5.png" class="img-medium" />

Define the details for the input:

1. Specify the name or the alias for the input: *KiZAN-IoT-Device-Reference-Data*
2. Set Source Type to *Reference Data*
3. Set import option to *Provide blob storage settings manually*
4. Set storage account to *kizandevices*
5. Storage account key: **Your storage account key will be provided during the workshop**
6. Set container to *referencedata*
7. Set path pattern to *DeviceReferenceData.csv*
8. Set event serialization format to *CSV*
9. Set delimiter to *comma (,)*
10. Set Encoding to *UTF-8*
11. Press the *Create* button

<img src="images/chapter4/Stream Analytics/StreamAnalytics 8.png" class="img-medium" />

Your inputs should now be properly configured.

<div class="exercise-end"></div>

### Define Outputs for your Stream Analytics Job

Your Stream Analytics Job will have two outputs: Power BI for real-time data visualization and Azure Data Lake Store for persistent storage of your telemetry data.

<h4 class="exercise-start">
    <b>Exercise</b>: Define Outputs
</h4>

> **NOTE:** Names and configuration settings described in this exercise must match those listed in the instructions.

#### Create the Azure Data Lake Output

Click on *Outputs* in the navigation pane for the Stream Analytics Job, and click on the *Add* button.
<img src="images/chapter4/Stream Analytics/StreamAnalytics 11.png" class="img-medium" />

Specify the details for the new output:
1. Set Output alias to *DataLakeStore*
2. Set Sink to *Data Lake Store*
3. Click on *Authorize* to authorize your output to connect to a Data Lake Store.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 12.png" class="img-small" />

Complete configuring the output:
1. Import option: *Select Data Lake Store from your subscription*
2. Subscription: Specify the name of your subscription.
3. Account name: Specify the name of your Azure Data Lake Store (it will be unique to your subscription)
4. Path prefix pattern: *telemetry/{date}*
5. Date format: *YYYY/MM/DD* (this format will ensure that telemetry data for each day will be stored in a separate folder)
6. Event serialization format: *JSON*
7. Encoding: *UTF-8*
8. Format: *Line separated*
9. Click the *Create* button

<img src="images/chapter4/Stream Analytics/StreamAnalytics 13.png" class="img-small" />


#### Create the Power BI Output

From the Outputs section of the Stream Analytics Job blade, click the *Add* button.
<img src="images/chapter4/Stream Analytics/StreamAnalytics 14.png" class="img-medium" />

Specify the details for the new output:
1. Set Output alias to *PowerBI*
2. Set Sink to *Power BI*
3. Click on *Authorize* to authorize your output to connect to your Power BI account.
<img src="images/chapter4/Stream Analytics/StreamAnalytics 15.png" class="img-small" />

A pop-up window will open allowing you to log into your Power BI Account.
<img src="images/chapter4/Stream Analytics/StreamAnalytics 16.png" class="img-medium" />

Finish setting up the Power BI output:
1. Set Group Workspace to *My workspace*
2. Set Dataset Name to *Device Telemetry*
3. Set Table Name to *Device Telemetry*
4. Click the *Create* button

<img src="images/chapter4/Stream Analytics/StreamAnalytics 17.png" class="img-small" />

Your outputs should now be properly configured.

<div class="exercise-end"></div>

### Define Machine Learning Function for your Stream Analytics Job

Your Stream Analytics Function will ingest streaming telemetry data from your connected electrical motors, combine telemetry data with device metadata (such as device types, maintenance history and operating characteristics), and predict the remaining useful life of the device. The prediction of the remaining useful life will be made by calling the Machine Learning Web Service that we have created in an earlier exercise.

<h4 class="exercise-start">
    <b>Exercise</b>: Define Machine Learning Function
</h4>

To get started, click on *Functions* in the navigation pane of the Stream Analytics Job blade.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 9.png" class="img-medium" />

Specify the details for the new function:
1. Set Function Alias to *RemainingUsefulLife*
2. Set Function Type to *Azure ML*
3. Set Import option to *Select from the same subscription*
4. Set URL to the name of the Machine Learning web service that you had created in your subscription
5. Click the *Create* button.

<div class="exercise-end"></div>

### Write a Query to Transform and Analyze Streaming Data

Stream Analytics Jobs use a SQL-like query language to define transformations for the streaming data. We will write a query that will perform the following tasks:
1. Summarize telemetry data for each 1-minute period
2. Summarize telemetry data for each 15-minute period
3. Summarize telemetry data for the past 24 hours
4. Join summarized telemetry data with a reference dataset containing device metadata and derive a variety of metrics, such as 
    * Run Time Since Maintenance
    * Run Time Since Overhaul
    * Run Time Since Production
    * Age Since Overhaul
    * Age Since Production
    * Average (mean) temperature over the latest 1-minute period
    * Standard deviation of temperature over the latest 1-minute period
    * Range of temperature over the latest 1-minute period                
    * Maximum temperature over the latest 1-minute period                
    * Average (mean) temperature over the latest 15-minute period
    * Standard deviation of temperature over the latest 15-minute period
    * Range of temperature over the latest 15-minute period                
    * Maximum temperature over the latest 15-minute period                
    * Number of observations exceeding the maximum operating temperature over the past 24 hours
5. Call the Machine Learning Web Service to get a prediction of remaining useful life
6. Send data to Power BI for real-time visualization
7. Send data to Data Lake Store for permanent storage.

<h4 class="exercise-start">
    <b>Exercise</b>: Create a Stream Analytics Query
</h4>

Click on *Query* in the navigation pane for the Stream Analytics Job. You will be directed to a query editor window where you will be able to specify a stream analytics query that will transform the streaming data:

<img src="images/chapter4/Stream Analytics/StreamAnalytics 19.png" class="img-large" />

If you are familiar with the Structured Query Language (SQL), you will be right at home with the Stream Analytics Query language. You will discover some constructs that are unique to this language. We encourage you to consult the [Stream Analytics Query Language Reference](https://msdn.microsoft.com/en-us/library/azure/dn834998.aspx) for additional details.

Copy the Stream Analytics Query shown below to your clipboard -- be sure to use the handy *Copy* button in the upper right corner of the code block. Then, paste the query into the query editor window, and press the *Save* button. 

````sql
--Summarize temperature data for each 1-minute period
WITH [TemperatureByDevice1Minute]  AS (
SELECT T.deviceId AS [Device Id],
    System.Timestamp AS [Event Time],
    AVG(CAST(T.tempF as float)) AS [TempF Mean - 1 Minute],
    STDEV(CAST(T.tempF as float)) AS [TempF StDev - 1 Minute],
    MAX(CAST(T.tempF as float)) - MIN(CAST(T.tempF as float)) AS [TempF Range - 1 Minute],
    MAX(CAST(T.tempF as float)) AS [TempF Max - 1 Minute]
FROM
    [KiZAN-IoT-Hub] T TimeStamp By [EventEnqueuedUtcTime]
WHERE T.tempF BETWEEN 50 AND 250
GROUP BY HoppingWindow(second, 60, 30),
    T.deviceId    
)

--Summarize temperature data for each 15-minute period
, [TemperatureByDevice15Minutes]  AS (
SELECT T.deviceId AS [Device Id],
    System.Timestamp AS [Event Time],
    AVG(CAST(T.tempF as float)) AS [TempF Mean - 15 Minutes],
    STDEV(CAST(T.tempF as float)) AS [TempF StDev - 15 Minutes],
    MAX(CAST(T.tempF as float)) - MIN(CAST(T.tempF as float)) AS [TempF Range - 15 Minutes],
    MAX(CAST(T.tempF as float)) AS [TempF Max - 15 Minutes]
FROM
    [KiZAN-IoT-Hub] T TimeStamp By [EventEnqueuedUtcTime]
WHERE T.tempF BETWEEN 50 AND 250
GROUP BY HoppingWindow(second, 900, 30),
    T.deviceId
)

--Summarize temperatures by device over a 24-hour period
, [TemperaturesByDevice24Hours] AS (
SELECT
    System.Timestamp AS [Time Stamp],
    T.[deviceId] AS [Device ID],
	CEILING(CAST(T.[tempF] as float)) AS [Temperature],
	MAX(CAST(T.[runTime] AS bigint)) AS [Run Time],
    COUNT(*) AS [Record Count]
FROM
    [KiZAN-IoT-Hub] T TimeStamp By [EventEnqueuedUtcTime]
WHERE T.tempF BETWEEN 50 AND 250
GROUP BY HoppingWindow(second, 86400, 30),
    T.[deviceId],
    CEILING(CAST(T.[tempF] as float))
)

--Summarize excessive temperature events over a 24-hour period
, [TemperatureAlertsByDevice24Hours] AS (
SELECT
    system.timestamp AS [Time Stamp],
    T.[Device ID],
    RD.[Motor Type],
    RD.[Device Type],
    MAX(T.[Run Time] - CAST(RD.[Maintenance Run Time] as bigint)) AS [Run Time Since Maintenance],
    MAX(T.[Run Time] - CAST(RD.[Overhaul Run Time] as bigint)) AS [Run Time Since Overhaul],
    MAX(T.[Run Time]) AS [Run Time Since Production],
    DATEDIFF(day, CAST(RD.[Overhaul Date] AS datetime), System.Timestamp) AS [Age Since Overhaul],
    DATEDIFF(day, CAST(RD.[Production Date] AS datetime), System.Timestamp) AS [Age Since Production],
    SUM(
        CASE WHEN T.Temperature > (CAST(RD.[Max Operating Temperature] as float))
        THEN T.[Record Count]
        ELSE 0
        END) AS [Observations Above Max Temp - 24 Hours]
FROM
    [TemperaturesByDevice24Hours] T
    INNER JOIN [KiZAN-IoT-Device-Reference-Data] RD
        ON T.[Device Id] = RD.[Device Id]
GROUP BY  system.timestamp,
    T.[Device ID],
    RD.[Motor Type],
    RD.[Device Type],
    RD.[Overhaul Date],
    RD.[Production Date]
)

, DataWithPredictions AS (
SELECT
    System.Timestamp AS [Time Stamp],
    T1M.[Device ID],
    T24H.[Motor Type],
    T24H.[Device Type],
    T24H.[Run Time Since Maintenance],
    T24H.[Run Time Since Overhaul],
    T24H.[Run Time Since Production],
    T24H.[Age Since Overhaul],
    T24H.[Age Since Production],
    --Summaries for each 1-minute period
    T1M.[TempF Mean - 1 Minute],
    T1M.[TempF StDev - 1 Minute],
    T1M.[TempF Range - 1 Minute],
    T1M.[TempF Max - 1 Minute],
    --Summaries for each 15 minute interval
    T15M.[TempF Mean - 15 Minutes],
    T15M.[TempF StDev - 15 Minutes],
    T15M.[TempF Range - 15 Minutes],
    T15M.[TempF Max - 15 Minutes],
    T24H.[Observations Above Max Temp - 24 Hours],
    --Call Azure Machine Learning web service to get a Remaining Useful Life prediction
    RemainingUsefulLife(
		T24H.[Motor Type],
		T24H.[Device Type],
		T24H.[Run Time Since Maintenance],
		T24H.[Run Time Since Overhaul],
		T24H.[Run Time Since Production],
		T24H.[Age Since Overhaul],
		T24H.[Age Since Production],
		T1M.[TempF Mean - 1 Minute],
		T1M.[TempF StDev - 1 Minute],
		T1M.[TempF Range - 1 Minute],
		T1M.[TempF Max - 1 Minute],
		T15M.[TempF Mean - 15 Minutes],
		T15M.[TempF StDev - 15 Minutes],
		T15M.[TempF Range - 15 Minutes],
		T15M.[TempF Max - 15 Minutes],
		T24H.[Observations Above Max Temp - 24 Hours]
        ) AS [Remaining Useful Life]
FROM
    [TemperatureByDevice1Minute] T1M
    INNER JOIN [TemperatureByDevice15Minutes] T15M
        ON T1M.[Device Id] = T15M.[Device Id]
        AND DATEDIFF(second,T1M,T15M) = 0
    INNER JOIN [TemperatureAlertsByDevice24Hours] T24H
        ON T1M.[Device Id] = T24H.[Device Id]
        AND DATEDIFF(second,T1M,T24H) = 0
)

--Push data with predictions to PowerBI
SELECT *
INTO [PowerBI]
FROM DataWithPredictions

--Store data with predictions in Azure Data Lake Store
SELECT *
INTO [DataLakeStore]
FROM DataWithPredictions
````

<div class="exercise-end"></div>

### Review and Start the Stream Analytics Job

<h4 class="exercise-start">
    <b>Exercise</b>: Review and Start the Stream Analytics Job
</h4>

By now, you have defined all major components of a Stream Analytics job, including the inputs, outputs, functions and query.

You can review a graphical diagram that illustrates the structure of your job by going to *Job Diagram* in the navigation bar.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 22.png" class="img-small" />

Take a moment to examine the diagram.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 20.png" class="img-large" />

Now, we are ready to star the Stream Analytics Job. Navigate to the Overview blade of the Stream Analytics Job and press the *Start* button. 

<img src="images/chapter4/Stream Analytics/StreamAnalytics 21.png" class="img-medium" />

You will be directed to a page that will allow you to specify the moment from which the job should start reading data from the data source. Select *Now* and press the *Start* button.

<img src="images/chapter4/Stream Analytics/StreamAnalytics 23.png" class="img-medium" />

It may take a couple of minutes for the Stream Analytics job to start. You will see a confirmation once the job has started successfully.

<div class="exercise-end"></div>