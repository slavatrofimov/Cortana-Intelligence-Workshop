## Build a Machine Learning Model

### Create a new resource group for the Predictive Maintenance Solution

<h4 class="exercise-start">
    <b>Exercise</b>: Create an Azure Resource Group
</h4>

Azure Resource groups are resources that serve as "containers" for collections of other resources. The benefit of resource groups is that they allow an Azure administrator to roll-up billing and monitoring information for resources within a resource group and manage access to those resources as a set. We will place all resources for the Predictive Maintenance solution into a common resource group.

Log into your Azure Portal by navigating to https://portal.azure.com.

<img src="images/chapter2/Resource Group/ResourceGroup 1.png" class="img-large" />

Click on the "+" sign in the upper left corner and type in the term "Resource Group" in the Search bar, then select "Resource Group" from the list of matching resource types.

<img src="images/chapter2/Resource Group/ResourceGroup 2.png" class="img-medium" />

Review the description of the resource you are about to create and press the *Create* button.

>**NOTE:** The process of finding a desired type of a new resource to be created is applicable to all types of resources. You will do this frequently throughout this workshop.

Enter the name of resource group, confirm subscription to which the resource group belongs and select a location for the resource group.

<img src="images/chapter2/Resource Group/ResourceGroup 4.png" class="img" />

Confirm that the resource group was created successfully.
<img src="images/chapter2/Resource Group/ResourceGroup 5.png" class="img-medium" />

<div class="exercise-end"></div>

### Create a Machine Learning Workspace
A key part of the predictive maintenance solution that we are about to build is a machine learning model that will estimate the useful life of an electrical motor based on various factors. This machine learning model will be designed in the Azure Machine Learning Studio. To use Azure Machine Learning Studio, you need to have a Machine Learning workspace, which contains the tools you need to create, manage, and publish advanced analytics solutions in the cloud, as well as collaborate with your colleagues on the development of these solutions.

As part of setting up a Machine Learning Workspace, we will also create a Machine Learning Web Service Plan. After you have developed an experiment in Machine Learning Studio, we will deploy the experiment as a web service hosted on Azure. The costs associated with web services are managed under web service pricing plans that you will select.

<h4 class="exercise-start">
    <b>Exercise</b>: Create a Machine Learning Workspace and Web Service Plan
</h4>

Click on the "+" sign in the upper left corner and type in the term "Machine Learning" in the Search bar, then select "Machine Learning workspace" from the list of matching resource types.

Review the description of the resource you are about to create and press the *Create* button.

<img src="images/chapter2/ML Workspace/MLWS 1.png" class="img-large" />

Specify the properties of the Machine Learning workspace.

1. Specify workspace name
2. Confirm the subscription for the workspace
3. Select the existing resource group
4. Select the desired location
5. Create a new storage account and provide the name for the account
6. Select "Standard" pricing tier
7. Create a new "Web service plan" and provide the name for the web service plan
8. Click to select a pricing tier for the web service plan
9. Click on the desired pricing tier
10. Click on the *Select* button to confirm pricing tier selection
11. Click on the *Create* button to provision the machine learning workspace

>**NOTE:**  Machine Learning Web Service Plans allow you to customize your costs based on the number of transactions and compute hours used by your active web services per month. A free DEVTEST Web service plan will be sufficient for the purposes of this workshop. However, you may need to upgrade to another tier depending on how much you use this web service.

<div class="exercise-end"></div>


### Create a Machine Learning Experiment
<h4 class="exercise-start">
    <b>Exercise</b>: Create a Machine Learning Experiment
</h4>

During this exercise, you will start developing a machine learning model using Azure Machine Learning Studio. The purpose of the model is to predict the remaining useful life of an electrical motor based on its attributes and operating conditions.

After logging into the Azure portal, navigate to the Machine Learning Workspace:

![Navigate to Machine Learning Workspace](images/chapter2/Machine Learning/ML Model 1.png)

From the Machine Learning Workspace overview blade, launch the Machine Learning Studio.

![Launch Machine Learning Studio](images/chapter2/Machine Learning/ML Model 3.png)

Sign into the Machine Learning Studio.

![Sign into the Machine Learning Studio](images/chapter2/Machine Learning/ML Model 5.png)

From the experiments area of the Machine Learning Studio, create a new Experiment.

![Create a new experiment](images/chapter2/Machine Learning/ML Model 6.png)

We will start with a blank experiment, by clicking the "Blank Experiment" tile, which will open a new experiment design area.

![Start with a blank experiment](images/chapter2/Machine Learning/ML Model 7.png)

The experiment design area consists of an experiment canvas in the center, a navigation bar with a list of available modules on the left and a properties pane on the right.

<div class="exercise-end"></div>

### Import Data

<h4 class="exercise-start">
    <b>Exercise</b>: Import Data
</h4>

We will add the first module to our machine learning experiment, which will import the raw data for the model. Expand the *Data Inputs and Outputs* folder, find the *Import Data* module and drag it onto the experiment canvas.

![Add the Import Data Module](images/chapter2/Machine Learning/ML Model 10.png)

Now, let's configure the Import Data Module by clicking on the *Launch Import Data Wizard*, and selecting *Web URL via HTTP* from the list of available sources.

![Launch Import Data Wizard](images/chapter2/Machine Learning/ML Model 11.png)

On the next step of the wizard, provide the Data Source URL:

https://kizanmltrainingdata.blob.core.windows.net/predictivemaintenance/Machine%20Learning%20-%20Remaining%20Useful%20life.csv
 
Select CSV data format and indicate that the CSV file has a header row:

<img src="images/chapter2/Machine Learning/ML Model 12.png" class="img-medium" />

Complete the Import Data Wizard configuration.

<img src="images/chapter2/Machine Learning/ML Model 14.png" class="img-medium" />

After configuring the data import wizard, let's run the experiment to make sure that the data can be imported.

<img src="images/chapter2/Machine Learning/ML Model 15.png" class="img-medium" />

You should see a green check mark indicating that the module has run successfully. Now, let's examine and visualize the content of the dataset that we have just imported by right-clicking on the Import Data module, clicking on "Results dataset" and clicking on "Visualize."

<img src="images/chapter2/Machine Learning/ML Model 21.png" class="img-medium" />

You will observe column and row counts, a sample of data, as well as histograms depicting the distribution of values in each column.

>**NOTE:** It is a good practice to review each column carefully to identify any anomalies or data quality issues that need to be addressed before training your machine learning model. You can click on the heading of each column to see basic descriptive statistics for column values, as well as a a more detailed histogram of value distribution. 

<img src="images/chapter2/Machine Learning/ML Model 26.png" class="img" />

Now that we know that the data has been imported successfully, let's configure the Import Data Module to *Use cached results*, since we do not expect our source data to change.

<img src="images/chapter2/Machine Learning/ML Model 18.png" class="img" />


#### Rename and Save the Draft of the Experiment
By default, our experiment is titled *Experiment created on {date}*. Let's give a more descriptive name to our experiment by selecting the current title in the title bar and replacing it with a more suitable title, such as *Predictive Maintenance*. 

<img src="images/chapter2/Machine Learning/ML Model 19.png" class="img-medium" />

We are now ready to save the draft of the experiment.

<img src="images/chapter2/Machine Learning/ML Model 20.png" class="img-small" />

<div class="exercise-end"></div>


### Prepare Data

<h4 class="exercise-start">
    <b>Exercise</b>: Edit Metadata of the Source Dataset
</h4>

While reviewing imported dataset, we noticed two columns containing categorical values (*Motor Type* and *Device Type*). Let's indicate that these columns contain categorical data to ensure that they are handled properly by various machine learning algorithms. To help us with this task, we will use the *Edit Metadata* module. Let's find this module by typing the phrase *Edit metadata* in the search bar. Then, let's drag the Edit Metadata module to the design surface of the experiment.

<img src="images/chapter2/Machine Learning/ML Model 23.png" class="img-medium" />

Connect the output of the *Import Data* module to the input of the *Edit Metadata* module. 

<img src="images/chapter2/Machine Learning/ML Model 24.png" class="img-small" />

Launch column selector.

<img src="images/chapter2/Machine Learning/ML Model 25.png" class="img-medium" />

Select *Motor Type* and *Device Type* columns:

<img src="images/chapter2/Machine Learning/ML Model 27.png" class="img-medium" />

Make selected columns categorical.

<img src="images/chapter2/Machine Learning/ML Model 27.5.png" class="img-small" />

<div class="exercise-end"></div>

<h4 class="exercise-start">
    <b>Exercise</b>: Clean Missing Data
</h4>

During the data preparation phase of the data science process, we may need to handle the possibility of encountering missing data in one or more columns of certain records. For this experiment, let's replace missing values with the average (mean) of other values in the corresponding column.

Find the *Clean Missing Data* module by typing the word *Clean* in the search bar. Then, drag the *Clean Missing Data* module onto the design surface.

<img src="images/chapter2/Machine Learning/ML Model 28.png" class="img-medium" />

Connect the output of the *Edit Metadata* module to the input of the *Clean Missing Data* module. 

<img src="images/chapter2/Machine Learning/ML Model 29.png" class="img-small" />

Launch column selector and select all columns, except for *Motor Type*, *Device Type* and *Remaining Useful Life*.

<img src="images/chapter2/Machine Learning/ML Model 30.png" class="img" />

Configure the cleaning mode to Replace missing values with the mean.

<img src="images/chapter2/Machine Learning/ML Model 31.5.png" class="img-small" />

<div class="exercise-end"></div>

<h4 class="exercise-start">
    <b>Exercise</b>: Split Source Data into a Training Set and Validation Set
</h4>

When we develop machine learning models, it may be possible to train a model that can make accurate predictions for those records that have been used to train the model. Yet, our objective is to train a model that can make accurate predictions for new data (data that the model has not previously seen). One of the simplest ways to simulate the "new" data is by splitting our original dataset into partitions:
1. The training set that will be used to train the model
2. The validation set that will be used to estimate the prediction error of the model

> **NOTE:** In more advanced data science processes, it is common to split the data into three sets: the training set that is used to train several models, the validation set that is used to estimate prediction error in order to select the best model, and the test set that is used to estimate the prediction error of the final model that gets selected. For simplicity, we will only use the training and validation sets in this experiment.

Find the *Split Data* module by typing the word *Split* in the search bar. Then, drag the module onto the design surface.

<img src="images/chapter2/Machine Learning/ML Model 32.png" class="img-medium" />

Connect the output of the *Clean Missing Data* module to the input of the *Split Data* module. 

<img src="images/chapter2/Machine Learning/ML Model 33.png" class="img-small" />

Configure the *Split Data* module by setting the fraction of rows in the first output dataset to 0.7

<img src="images/chapter2/Machine Learning/ML Model 34.png" class="img-small" />

<div class="exercise-end"></div>

### Train the Machine Learning Model

<h4 class="exercise-start">
    <b>Exercise</b>: Train the Machine Learning Model
</h4>

Find the *Train Model* module by typing the phrase *Train Model* in the search bar. Then, drag the module onto the design surface.

<img src="images/chapter2/Machine Learning/ML Model 35.png" class="img-medium" />

Connect the first output of the *Split Data* module to the second input of the *Train Model* module. 

<img src="images/chapter2/Machine Learning/ML Model 36.png" class="img-small" />

We will use the *Boosted Decision Tree Regression* to predict the Remaining Useful Life of electrical motors. Let's initialize the machine learning model by selecting the appropriate algorithm and specifying the algorithm parameters.

>**NOTE:** The process of selecting a suitable algorithm and the selection of optimal algorithm parameters is a crucial part of the data science process. While some algorithms may be suitable for certain types of machine learning problems, it is often necessary to try and compare multiple algorithms and multiple combinations of algorithm parameters. For simplicity, we will only use a single algorithm with a basic set of parameters in this exercise.

Find the *Boosted Decision Tree Regression* module by typing the word *Boosted* in the search bar. Drag the module onto the design surface. Then, drag the output of the *Boosted Decision Tree Regression* module to the first input of the *Train Model* module. 

<img src="images/chapter2/Machine Learning/ML Model 38.png" class="img" />

Configure the *Train Model* module by launching the column selector and selecting the *Remaining Useful Life* column (as the variable to be predicted).

<img src="images/chapter2/Machine Learning/ML Model 40.png" class="img-medium" />

Configure the parameters of the *Boosted Decision Tree Regression* module as illustrated below:

<img src="images/chapter2/Machine Learning/ML Model 47.png" class="img-small" />

<div class="exercise-end"></div>

### Score and Evaluate the Machine Learning Model

<h4 class="exercise-start">
    <b>Exercise</b>: Score the Machine Learning Model
</h4>

During the scoring process, we will use the newly trained Boosted Decision Tree Regression model to predict the remaining useful life of records in the validation dataset.

Find the *Score Model* module by typing the phrase *Score Model* in the search bar. Drag the module onto the design surface. 

<img src="images/chapter2/Machine Learning/ML Model 43.png" class="img" />

Drag the output of the *Train Model* module to the first input of the *Score Model* module. Then, drag the second output of the *Split Data* module to the second input of the *Score Model* module.

<img src="images/chapter2/Machine Learning/ML Model 43.png" class="img-medium" />

Configure the *Score Model* module by ensuring that the *Append score columns to output* option is checked.

<img src="images/chapter2/Machine Learning/ML Model 42.png" class="img-medium" />

<div class="exercise-end"></div>

<h4 class="exercise-start">
    <b>Exercise</b>: Evaluate the Machine Learning Model
</h4>

To evaluate the machine learning model, we will compare the predictions of remaining useful life made by the model with actual remaining useful life of motors in our validation dataset.

Find the *Evaluate Model* module by typing the word *Evaluate* in the search bar. Drag the module onto the design surface. Then, connect the output of the *Score Model* module to the first input of the *Evaluate Model* module.

<img src="images/chapter2/Machine Learning/ML Model 45.png" class="img" />

#### Run the Machine Learning Experiment

Now that the machine learning model is built, we can run the entire experiment.

Press the *Run* button at the bottom of the screen and click the *Run* button in the pop-up menu to run the entire experiment.

<img src="images/chapter2/Machine Learning/ML Model 46.png" class="img-medium" />

<div class="exercise-end"></div>

### Review and Save the Machine Learning Model

<h4 class="exercise-start">
    <b>Exercise</b>: Review the Machine Learning Model
</h4>

After running the experiment, we can review the accuracy of the machine learning model. Right-click on the *Evaluate Model* module. Click on *Evaluation results* and click on *Visualize*.

<img src="images/chapter2/Machine Learning/ML Model 50.png" class="img-medium" />

You will observe a summary describing the error rate of the machine learning model you had built.

<img src="images/chapter2/Machine Learning/ML Model 51.png" class="img-medium" />

You may also visualize the decision trees that have been constructed while training the Machine Learning model. Right-click on the *Train Model* module. Click on *Trained Model* and click on *Visualize*.

<img src="images/chapter2/Machine Learning/ML Model 52.png" class="img-medium" />

You will see a screen with a list of all decision trees, and the capabilities for interactive exploration of the splits in the decision tree.

<img src="images/chapter2/Machine Learning/ML Model 53.png" class="img-medium" />

#### Save the Machine Learning Experiment

Confirm that your completed experiment looks similar to the following diagram.

<img src="images/chapter2/Machine Learning/ML Model 55.png" class="img-medium" />

Save the experiment.

<img src="images/chapter2/Machine Learning/ML Model 48.png" class="img-medium" />

<div class="exercise-end"></div>

### Create a Machine Learning Web Service

After creating and training the machine learning model, we will operationalize the model by creating a Web Service that will enable us to make predictions of remaining useful life of electrical motors. Later on, we will use this web service in conjunction with a Stream Analytics job to predict and track the health of electrical motors in near-real-time.

<h4 class="exercise-start">
    <b>Exercise</b>: Create a Machine Learning Web Service
</h4>

If necessary, open the machine learning experiment that you had created in the previous section. Then, click on the *Set Up Web Service* button and click on *Predictive Web Service [Recommended]*.

<img src="images/chapter2/Machine Learning/ML Model 49.png" class="img-medium" />

Machine Learning Studio will automatically generate a Web Service experiment based on the model that you had previously created, which will look as follows:

<img src="images/chapter2/Machine Learning/ML Model 54.png" class="img" />

We will need to make several modifications to this draft of the Web Service experiment to customize it for our needs.

#### Adjust Web Service Input Parameters
First, we will need to make sure that remaining useful life is not expected as a web service parameter. Rearrange the layout of modules in the predictive experiment and remove the connection between the *Import Data* module and the *Edit Metadata* module.

<img src="images/chapter2/Machine Learning/ML Model 70.png" class="img-medium" />

Find the *Select Columns in Dataset* module by typing the phrase *Select Columns* in the search bar. Drag the *Select Columns in Dataset* module onto the design surface and place it between the *Import Data* and *Edit Metadata* modules. Connect the output of the *Import Data* module to the input of the *Select Columns in Dataset* module.

<img src="images/chapter2/Machine Learning/ML Model 71.png" class="img-medium" />

Launch column selector and exclude the *Remaining Useful Life* column from the dataset.

<img src="images/chapter2/Machine Learning/ML Model 72.png" class="img" />

Connect the output of the *Select Columns in Dataset* module to the input of the *Edit Metadata* module.

<img src="images/chapter2/Machine Learning/ML Model 73.png" class="img-medium" />

#### Adjust Web Service Outputs
Let us adjust the outputs of the web service such that it returns only the predictions of the remaining useful life and no other data.

First, remove the connection between the *Score Model* module and the *Web service output* module.

<img src="images/chapter2/Machine Learning/ML Model 56.png" class="img-small" />

Find the *Select Columns in Dataset* module by typing the phrase *Select Columns* in the search bar. Drag the *Select Columns in Dataset* module onto the design surface and place it between the *Score Model* module and the *Web service output* modules. Connect the output of the *Score Model* module to the input of the *Select Columns in Dataset* module.

<img src="images/chapter2/Machine Learning/ML Model 57.png" class="img-medium" />

Launch column selector and include the *Scored Labels* column from the dataset (while excluding all others).

<img src="images/chapter2/Machine Learning/ML Model 58.png" class="img" />

Connect the output of the *Select Columns in Dataset* module to the input of the *Web service output" module.

<img src="images/chapter2/Machine Learning/ML Model 59.png" class="img-small" />

#### Review, run and save the experiment
Your predictive experiment should now look something like the following diagram:

<img src="images/chapter2/Machine Learning/ML Model 75.png" class="img-medium" />

Let's run the entire predictive experiment:

<img src="images/chapter2/Machine Learning/ML Model 60.png" class="img-medium" />

Save the predictive experiment.

<img src="images/chapter2/Machine Learning/ML Model 48.png" class="img-medium" />

<div class="exercise-end"></div>

### Deploy Predictive Web Service

<h4 class="exercise-start">
    <b>Exercise</b>: Deploy the Predictive Web Service
</h4>

Once the predictive experiment has been run, deploy the predictive web service. Press the *Deploy Web Service* button and click *Deploy Web Service [New] Preview*.

<img src="images/chapter2/Machine Learning/ML Model 62.png" class="img-medium" />

Specify the name, storage account and price plan for the web service. Then, click *Deploy*.

<img src="images/chapter2/Machine Learning/ML Model 63.png" class="img-medium" />

You will be redirected to the web service management portal. Click on the *Use Web Service* link.

<img src="images/chapter2/Machine Learning/ML Model 64.png" class="img-medium" />

In the list of basic consumption information, note the *Primary Key* and *Request-Response* values - you would use these values to access your Machine Learning Web Service programmatically. You do not need to record these values for the purposes of this workshop.

<img src="images/chapter2/Machine Learning/ML Model 65.png" class="img" />

<div class="exercise-end"></div>