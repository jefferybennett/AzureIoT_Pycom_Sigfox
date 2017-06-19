<img src ="https://github.com/jefferybennett/AzureIoT_Pycom_Sigfox/blob/master/imgs/pycomlogo.png" width="300">
<img src ="https://github.com/jefferybennett/AzureIoT_Pycom_Sigfox/blob/master/imgs/azureiotlogo.png" width="300">
<img src ="https://github.com/jefferybennett/AzureIoT_Pycom_Sigfox/blob/master/imgs/sigfoxlogo.png" width="300">

# Microsoft Azure IoT, Pycom and Sigfox IoT Lab

Welcome! This workshop help you get up and running with data flowing into Microsoft Azure from the Pycom
SiPy device flowing through Sigfox.

# Start Here!

This set of instructions follows those provided by Pycom and Sigfox.  You can find these instructions here:

- [Pycom Lab Instructions](https://github.com/pycom-education/pycom-workshop-sf)
- [Sigfox Lab Instructions](https://github.com/aureleq/sigfox-azure-iothub)

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
However, if you'd prefer to skip using the Remote Monitoring solution, or have another way of viewing the data
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

## Use the Azure IoT Device Explorer to register your device and monitor data coming from it.

- (If you have not already done so) Download and install the [Azure IoT Device Explorer](https://github.com/Azure/azure-iot-sdks/releases/download/2016-11-17/SetupDeviceExplorer.msi)
on to a Windows computer.
- Open the Device Explorer.
- In your IoT Hub's blade in the Azure Management Portal, click the Shared Access Policies tab.
- Click the "iothubowner" policy.
- Copy the primary Connection string.
- Paste the connection string in the IoT Hub Connection String field on the Configuration tab of the Device Explorer
and click the Update button.
- Click the Data tab.
- Select your device in the Device ID dropdown, click the Enable checkbox next to Consumer Group and enter your first name.
(A consumer group using your first name will have been pre-created)

```text
HostName=amatiotthons1.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey=qh/9k+LOOO+RBf9XVdO4w8q/LSZIUQVXttBzIU48ifM=
```

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

## VNC to Raspberry PI and run AMAT Data Simulator
- After connecting to the Raspberry Pi via VNC, open a Terminal Window.
- Your terminal window will open to the root directory.
- Enter the command:
    ```text
    cd amatiotconsole
    ```
- Enter the command:
    ```text
    git pull origin master
    ```
- Enter the command:
    ```text
    npm install
    ```
- Enter the command:
    ```text
    node .
    ```

## Create the Azure Stream Analytics Job

### Create the Job
- Add a Stream Analytics job to your resource group, using the following selections:
    - Job name: Provide a name for the Stream Analytics job.
    - Region: Select the appropriate Microsoft Data Center location.
    - Regional Monitoring Storage Account: Depending upon your selected region, you'll be able to select a storage account
    for Stream Analytics to store service monitoring data. It's ok if this isn't available in your region.
- Click the Create button to create the job.

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

Here's a sample query that leverages all three outputs described in this lab:

```sql
With RawTelemetry AS (
    SELECT *,
        DateAdd(hour, -7, System.TimeStamp) as EventDateTime
    FROM
        iothub TIMESTAMP BY EventProcessedUtcTime
),
RawTelemetryGroupedByMinute AS (
    SELECT
        DeviceId,
        DateAdd(hour, -7, System.TimeStamp) as EventDateTime,
        Avg(T1) As AvgT1, 
        Avg(T2) As AvgT2,
        Avg(Frequency) AS AvgFrequency,
        Avg(Pressure) As AvgPressure
    FROM
        RawTelemetry 
    Group By DeviceId, EventDateTime, TumblingWindow(minute, 1)
),
Alarms AS (
    SELECT DeviceId, DateAdd(hour, -7, System.TimeStamp) as EventDateTime, 'HighTemperatureAlarm' As AlarmType,
    CONCAT('High T1 identified on Device ', DeviceId, ' over last 5 minutes.') as AlarmDetail,
    COUNT(*) AS EventCount
    FROM RawTelemetryGroupedByMinute
    WHERE AvgT1 > 100
    GROUP BY DeviceId, TumblingWindow(Duration(minute, 5)) 
    HAVING EventCount > 2
)

select * into powerbiraw from RawTelemetryGroupedByMinute
select * into powerbiaverage from RawTelemetryGroupedByMinute
select * into powerbialarm from Alarms
```

