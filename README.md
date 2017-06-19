<img src ="https://github.com/jefferybennett/AzureIoT_Pycom_Sigfox/blob/master/imgs/pycomlogo.png" width="300">
<img src ="https://github.com/jefferybennett/AzureIoT_Pycom_Sigfox/blob/master/imgs/azureiotlogo.png" width="300">
<img src ="https://github.com/jefferybennett/AzureIoT_Pycom_Sigfox/blob/master/imgs/sigfoxlogo.png" width="300">

# Microsoft Azure IoT, Pycom and Sigfox IoT Lab

Welcome! This workshop help you get up and running with data flowing into Microsoft Azure from the Pycom
SiPy device flowing through Sigfox.

# Start Here!

This set of instructions follows those provided by Pycom and Sigfox.  You can find these instructions here:

- [Pycom Lab Instructions](https://github.com/pycom-education/pycom-workshop-sf)

As you follow the Sigfox instructions, you may need to follow the instructions below to set-up
your Microsoft Azure account, if you don't already have one.

Thus, the instructions below assume you've accomplished the following:

1.  Set-up your Pycom SiPy device and having it sending data to Sigfox.
2.  Set-up your Sigfox account.

# Setting up your Microsoft Azure Account

If you don't already have one, you'll need to set-up a Microsoft Azure tenant.  If you're participating in a
guided lab with Microsoft, they may provide you a code with a free Azure credit.  Alternatively, you may be
eligible for a free $200 credit [here](https://azure.microsoft.com/en-us/free/).

### Create Windows Live Id
If you don't already have a Microsoft account, you can create one at [www.live.com](www.live.com).

### Utilize Azure Credit
After you've created and logged into your Microsoft account, go to [www.microsoftazurepass.com](www.microsoftazurepass.com)
and follow the instructions to set-up your Microsoft Azure environment.  If you're attending the June 19th, 2017 event in
San Francisco, e-Mail Jeff Bennett at jbennett@microsoft.com to receive the code for your Azure credit.

# Software Requirements

For this lab, we'll use the Azure IoT Suite Remote Monitoring solution to view the data flowing from our Pycom device.
However, if you'd prefer to skip using the Remote Monitoring solution, or would like another way of viewing the data
flowing from your device, you can install the Azure IoT Device Explorer (for Windows users) or, alternatively,
the Azure IoT Hub Explorer for Non-Windows users with Node.js installed.

- For Windows Users: Azure IoT Device Explorer
    - Download and install the [Azure IoT Device Explorer](https://github.com/Azure/azure-iot-sdks/releases/download/2016-11-17/SetupDeviceExplorer.msi) on
    to a Windows computer.
    - The Device Explorer will be used to connect to Azure IoT Hub to register devices and monitor
    the real-time data coming from them.
- For Non-Windows Users w/ Node.js installed: Azure IoT Hub Explorer
    - Download and install the Azure IoT Hub Explorer using the instructions found [here]
    (https://github.com/Azure/iothub-explorer).

# Set-up Azure IoT Suite Remote Monitoring Solution
Microsoft Azure IoT Suite is a set of pre-configured IoT solutions which can be quickly spun up in an Azure environment.  For this
lab, we'll be using the Remote Monitoring solution.

- In your browser, navigate to [www.azureiotsuite.com](www.azureiotsuite.com).
- Log-in using your credentials associated to your Azure environment.
- Click the box titled "Create a new solution".
- Select the Remote Monitoring solution.
- In the "Create Remote monitoring solution" page ...
    - Enter an unique solution name in the Solution name field.
    - Select your Azure subscription in the Subscription dropdown.  If you're using a free Azure Pass credit, the 
    subscription will be titled "Azure Pass".
    - Select the Azure region where this solution will run.
    - At the bottom of the page, click the "Create Solution" button.
- The provisioning process typically takes 5 - 10 minutes to complete.

Once the provisioning process is complete, you can click the "Launch" button under the "Provisioned solutions" page.

You can also navigate to https://[solution name].azurewebsites.net/Dashboard/Index

# Register your Pycom device with Azure IoT
Every device which communicates with Azure IoT must be registered, specifically with the Azure IoT Hub service.  By
registering your device, you create an unique registry entry and identity for the device (allowing, for example,
per device authentication to Azure IoT Hub).

### Register device using the Azure IoT Suite Remote Monitoring portal
The Remote Monitoring portal provides a mechanism to register devices with its associated Azure IoT Hub service.

- Open the Azure IoT Suite Remote Monitoring portal (if you've not already done so.)
- In the lower left-hand corner of the portal, click "Add a Device".
- Under "Simulated Device", click the "Add New" button.
- Click the "Let me define my own Device ID" radio button.
- Enter a device id in the "Enter a Device ID" textbox and click the "Check ID" button.
    - Device id's in Azure IoT must be unique and are also case-sensitive.
- Click the "Create" button.
- For easy reference, copy the "Device ID", "IoT Hub Hostname", and "Device Key" attributes to an easily referencable location
on your computer (eg. Notepad, etc.).

For reference, the Azure IoT Hub device connection string, would then be the following ...
```text
HostName=[IoT Hub Hostname];DeviceId=[Device ID];SharedAccessKey=[Device Key]
```

### Register device using Device Explorer or Hub Explorer
You can also register devices using the Device Explorer or Hub Explorer.  However, if you're using the Azure Iot Suite
Remote Monitoring solution, you'll want to register the device in the Remote Monitoring portal.

# Locate your Azure IoT Hub iothubowner connection string
The Azure IoT Hub iothubowner connection string can be used by various clients to connect to the Azure IoT Hub instance
with full permissions.  You'll need this connection string if you're using the Device Explorer or Hub Explorer.

- In the Azure management portal at [https://portal.azure.com](https://portal.azure.com) ...
    - Navigate to your Azure IoT Hub's configuration blade.
    - In your IoT Hub's blade, click the Shared Access Policies tab.
    - Click the "iothubowner" policy.
    - Copy the primary Connection string)

## Use the Azure IoT Device Explorer to monitor data coming from your Device

- Download and install the [Azure IoT Device Explorer](https://github.com/Azure/azure-iot-sdks/releases/download/2016-11-17/SetupDeviceExplorer.msi)
- Open the Device Explorer.
- In your IoT Hub's blade in the Azure Management Portal, click the Shared Access Policies tab.
- Click the "iothubowner" policy.
- Copy the primary Connection string.
- Paste the connection string in the IoT Hub Connection String field on the Configuration tab of the Device Explorer
and click the Update button.
- Click the Data tab.
- Select your device in the Device ID dropdown, click the Enable checkbox next to Consumer Group and enter your first name.
(A consumer group using your first name will have been pre-created)

# Analyze and Visualize Device Data Real-Time
In this section, we'll build on to the capabilities provided by the Azure IoT Remote Monitoring solution
by analyzing our device data stream real-time and streaming it real-time to Microsoft Power BI.

## Create the Azure Resource Group
Azure Resource Group's provide a number of useful capabilities. One of the primary is to organize your Azure service instances into
logical groups. Creating a single Resource Group that you'll use for this effort will prove very valuable.

- In the [Azure Management Portal](https://portal.azure.com):
    - Click the +New icon in the upper left corner.
    - Enter the search term 'Resource' in the search field. The option 'Resource Group' should immediately appear.
    - Then select Resource Group in the search listing and the Create button in the next blade.
    - In the Create Resource Group blade, complete the following fields:
        - Resource group name: Provide a name for your resource group. Pick a name that appropriately describes the purpose of
        resource group which you'll easily remember. For the lab, adding your name is good practice.
        - Subscription: Ensure the correct Azure subscription is selected.
        - Resource group location: Ensure the correct Azure DataCenter location is selected.
        - Click the Create button.

As you add additional Azure services, it's often easiest to simply add them directly from the Resource Group using the
Add button at the top of your Resource Group blade.

## Create the Azure Stream Analytics Job

### Create the Job
- From your newly create Azure Resource group, click the Add+ icon in the top middle.
- In the "Search Everything" textbox, enter "Stream Analytics job".  Select "Stream Analytics job" in the resultset dropdown.
- Click "Stream Analytics job" in the "Results" resultset, and "Create" in the newly opened blade.
- In the "New Stream Analytics Job" blade, using the following selections:
    - Job name: Provide a name for the Stream Analytics job.
    - Region: Select the appropriate Microsoft Data Center location.
    - Regional Monitoring Storage Account: Depending upon your selected region, you'll be able to select a storage account
    for Stream Analytics to store service monitoring data. It's ok if this isn't available in your region.
- Click the Create button to create the job.
- Navigate back to your Resource Group and click the Refresh button to view your newly created Stream Analytics job.

The job will take a few minutes to deploy, after which you can select it your list of Stream Analytics jobs by clicking
the arrow next to its name.

### Add an input
- After selecting the job in Stream Analytics list, select Inputs.
- Click the Add Input icon in the bottom menu.
- In the Add an Input dialog, complete the following:
    - Select Data Stream and click the right arrow.
    - Select IoT Hub and click the right arrow.
    - In IoT Hub settings, complete the following fields:
        - Input Alias: Provide an alias for your input which you'll use to refer to it in your query.
        - Subscription: Select the appropriate Azure subscription.
        - Choose an IoT Hub: You should be able to select from a dropdown of existing IoT Hub instances. This will
        then provide default values for the remaining fields.
    - Click the right arrow.
    - Review serialization settings and click the complete checkmark icon.

### Adding Outputs
To add Ouputs to your Stream Analytics job, you'll need to be in the Job and then click Outputs.

#### Add the Power BI Output
The following documentation can assist in leveraging Stream Analytics with Power BI,
located [here](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-power-bi-dashboard).

- In the bottom menu, click the Add Output icon.
- Select Power BI, and click the right arrow icon.
- In Authorize Connection, click the Authorize Now link and enter the credentials for the Office 365 account you wish
to use for Power BI. Ensure you click the Sign-In button and that your credentials are successfully authorized and accepted.
    - If you do not have an Office 365 instance available to you, your lab guide will provide you one.
- In Microsoft Power BI Settings, complete the following fields:
    - Output alias: Provide an alias for your output which you'll use to refer to it in your query.
    - Dataset name: Provide a name of your dataset to be created in Power BI.
    - Table name: Provide a name of your table to be created in the dataset.
    - Workspace: Select the workspace in Power BI where the dataset and table will be created.
    - Click the checkmark icon to complete.

### Write the Query
To write/edit your query, you'll need to be in the Stream Analytics Job and then click Query. While you can certainly use
the Management Portal query window to write and edit your query, I find it a best practice to leverage a tool like
[Visual Code](https://code.visualstudio.com) to write your query first, especially because I can leverage a source control
platform like GitHub to place it under source control.

The simplest query is to simply pass the data from input to your output.  You can leverage the default query and then change your input and output aliases to those you entered when creating your IoT Hub input and Power BI output ...
```sql
SELECT
    DeviceId,
    DateAdd(hour, -7, System.TimeStamp) as EventDateTime,
    CAST(Temperature as bigint) as CurrentTemperature,
    CAST(Humidity as bigint) as CurrentHumidity
INTO
    [YourOutputAlias]
FROM
    [YourInputAlias]
```

# Setting Up your Power BI Dashboard
Power BI is Microsoft's Enterprise Data Visualization platform.

- Navigate to [Power BI](https://powerbi.com).
- To sign in, you'll need an Office 365 account.  If you don't have access to an Office 365 account, your Microsoft lab guide
will provide you one.
- Click on the "My Workspace" icon in the left-hand navigation.
- Click on the tab "Datasets".
- Click on the "Create Report" icon under the column "Actions".
