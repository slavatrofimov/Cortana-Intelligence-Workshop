## Visualize Streaming Data With Power BI

Once the Stream Analytics got started, it created a streaming dataset in your Power BI account and started pushing data to the data set. We are ready to develop Power BI reports and dashboards to visualize the data.

### Create a Power BI Report
<h4 class="exercise-start">
    <b>Exercise</b>: Create a Power BI Report
</h4>

Log into your Power BI account by navigating to https://app.powerbi.com and logging in with your username and password. After logging in you will see the content of your personal workspace. Click on the down-arrow next to the *My Workspace* link to expand the navigation menu for your workspace.

<img src="images/chapter5/Power BI/PowerBI 2.png" class="img-large" />

You should see a list of *Dashboards*, *Reports*, *Workbooks* and *Datasets*. You should see a *Device Telemetry* dataset among your datasets. Click on the *Device Telemetry* dataset.

<img src="images/chapter5/Power BI/PowerBI 3.png" class="img-small" />

> **NOTE:** Unless you have previously created reports, dashboards, workbooks, or other datasets, you will not see any other content in your workspace. 

After click on the *Device Telemetry* dataset, you will see a blank report based on this dataset.

<img src="images/chapter5/Power BI/PowerBI 4.png" class="img-large" />

The report design area consists of several main sections:
* Report canvas that serves as the primary design area for your report.
* Visualizations pane that allows you to add and configure visuals for the report
* Filters pane that allows you to specify relevant filters for your report
* Fields pane that lists tables and fields that comprise your dataset.

Let's add the first visual to the report:
1. Drag the *Line chart* visual to the report canvas
2. Resize the visual to make it larger, and make sure that the line chart visual is selected.
3. Find the *time stamp* field in the Fields pane.
4. Drag the *time stamp* field to the *Axis* placeholder for your line chart.
5. Find the *device id* field in the Fields pane.
6. Drag the *device id* field to the *Legend* placeholder for your line chart.
7. Find the *tempf mean - 1 minute* field in the Fields pane.
8. Drag the *tempf mean - 1 minute* field to the *Values* placeholder for your line chart.

At this point you should see a chart that resembles the one shown below:
<img src="images/chapter5/Power BI/PowerBI 5.png" class="img-large" />

Let's save your report by expanding the *File* menu and clicking on *Save*.

<img src="images/chapter5/Power BI/PowerBI 6.png" class="img-small" />

You will be asked to provide the name for your new report. Let's label it *Device Telemetry*.

<img src="images/chapter5/Power BI/PowerBI 7.png" class="img-medium" />

<div class="exercise-end"></div>

### Create a Power BI Dashboard

Power BI allows you to combine a set of visuals from one or more reports on a dashboard. By combining visuals from multiple reports, the dashboard can provide a convenient, comprehensive picture of a variety of business processes. Power BI dashboards also provide an ideal way of visualizing streaming data, since the dashboard can be refreshed in near-real-time as new records arrive.

<h4 class="exercise-start">
    <b>Exercise</b>: Create a Power BI Dashboard
</h4>

First, open the *Device Telemetry* report that you have created in the previous exercise. 

Then, find and click the Pin icon in the upper right corner of the line chart representing device temperatures over time. This icon will allow you to add a visual to a dashboard.

<img src="images/chapter5/Power BI/PowerBI 8.png" class="img-small" />

Indicate that you would like to pin the visual to a new dashboard, specify *Device Telemetry* as the name of the dashboard, and press the *Save* button.

<img src="images/chapter5/Power BI/PowerBI 9.png" class="img-medium" />

Once your dashboard has been created, click on *Device Telemetry* from the list of dashboards in your navigation bar, which will bring you to the Device Telemetry dashboard.

<img src="images/chapter5/Power BI/PowerBI 10.png" class="img" />

As you observe the dashboard, you will notice that the data on the dashboard will refresh automatically as new records are pushed by the Stream Analytics job to the streaming dataset in Power BI. No manual actions are necessary to refresh the data. 

<img src="images/chapter5/Power BI/Power BI - Streaming Data Viz.gif" class="img" />

> **NOTE:** The animation above is accelerated. You should expect to see your streaming dataset refresh every 30 seconds, due to the fact that your Stream Analytics job is configured to output events every 30 seconds.

<div class="exercise-end"></div>


### Enhance your Power BI Report and Dashboard

Power BI provides a rich environment for authoring reports, visualizing data and performing exploratory data analysis. While the simple report that we created in one of the previous exercises is sufficient to illustrate the concepts of report development in Power BI, you may want to experiment with creating more advanced reports. The purpose of the following exercise is to encourage independent exploration of features and capabilities of Power BI.

<h4 class="exercise-start">
    <b>Optional Exercise</b>: Enhance Power BI Report and Dashboard
</h4>

First, add several new visuals to the Power BI report, such as:
* Another line chart that illustrates estimated remaining useful life by device over time.
* A bar chart that illustrates highest temperature by device type
* A bar chart that illustrates highest temperature by motor type
* A slicer that allows filtering the content by time stamp
* A slice that allows filtering the content by device id
* A text box that represents the title of the report page

When you are finished, your report should look similar to the following illustration.

<img src="images/chapter5/Power BI/PowerBI 12.png" class="img-large" />

Once you have enhanced the report, pin the visual that represents estimated remaining useful life by device over time to the *Device Telemetry* dashboard. 

Your enhanced dashboard should look similar to the illustration below:

<img src="images/chapter5/Power BI/PowerBI 14.png" class="img-large" />

<div class="exercise-end"></div>