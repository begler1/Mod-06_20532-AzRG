
<!---
Version: 1.0 
-->
# Exercise 1: Populating the Sign-In Form with Registrant Names
## INTRODUCTION MESSAGE
In this exercise, you will:  
  
Query table entities by using a CloudTableClient instance.  
Use LINQ-to-Objects on a set of entities.  
  
The main tasks for this exercise are as follows:  
  
Create an instance of the CloudTable class.  
Retrieve strongly-typed registration records by partition key.  
Use LINQ-to-Objects to project a list of registrant names.
## COMPLETION MESSAGE
Results: After completing this exercise, you will have queried entities by row key or partition key from Table storage.
### Login as Student
Login as Student with a password of Pa$$w0rd.

#### :bulb: KNOWLEDGE
You can use the Commands menu and choose Ctrl\+Alt\+Delete then click Student and enter Pa$$w0rd and press Enter. You can also use the Command menu and choose Paste/Paste Password instead of typing the password manually.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773341.jpg
>* ShowAutomatically = No





### On the Start screen, click Internet Explorer
On the Start screen, click the Internet Explorer tile.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773342.jpg
>* ShowAutomatically = No





### Go to the new Azure Portal
Go to https://portal.azure.com. Enter the email address of your Microsoft account associated with your Azure subscription. Then enter the password for your Microsoft account. Check Keep me signed in. Click Sign In.

#### :bulb: KNOWLEDGE
Before starting this lab, you must have completed the lab in Module 2. All work in this lab is done within vm20532 created in the lab in Module 2. Start and Connect via Azure Portal.  
  
If you see a pop-up for Skype for Business click Don't Enable.  
  
Ignore any updates to OneDrive.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666469.jpg
>* ShowAutomatically = No



#### :calling: COMMAND
```TypeText
https://portal.azure.com
```


### Browse Virtual Machines
In the navigation pane on the left side of the Azure Portal, click Virtual Machines.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666470.jpg
>* ShowAutomatically = No





### Start the VM
Click the vm20532 VM that was created in the lab in Module 2 for development. In the Overview blade, if the VM is stopped, click Start and wait for the VM to start up. This may take a few minutes.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666471.jpg
>* ShowAutomatically = No





### Connect to the VM via RDP
When the vm20532 VM has started, click Connect. You may have to click the Refresh button first.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666472.jpg
>* ShowAutomatically = No





### Allow pop-ups
If presented with a message box that shows a pop-up has been blocked, select Options for this site and choose Always Allow. Then click Connect again.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/672208.jpg





### Click Open
When presented with the RDP download pop-up at the bottom of the screen, click Open.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/672209.jpg





### In the Remote Desktop Connection dialog box:
In the Remote Desktop Connection dialog box, perform the following steps:  
a. Click Don’t ask me again for connections to this computer to prevent this dialog box from displaying again.  
b. Click Connect.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666473.jpg
>* ShowAutomatically = No





### In the Windows Security dialog box:
In the Windows Security dialog box, perform the following steps:  
a. For the User name dialog box, provide the value, Student. b. For the Password dialog box, provide the value, AzurePa$$w0rd. c. Click OK.

#### :bulb: KNOWLEDGE
Note: If you computer is on a domain, you may need to add a backslash before the username to "escape" the domain.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666474.jpg
>* ShowAutomatically = No





### In the Remote Desktop Connection dialog box:
In the Remote Desktop Connection dialog box, perform the following steps:  
a. Verify if the Remote certificate name matches the name of your virtual machine. b. Click Don’t ask me again for connections to this computer to prevent this dialog box from displaying again. c. Click Yes.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666475.jpg
>* ShowAutomatically = No





### Minimize Server Manager
If you just started the VM, Server Manager will start automatically after 60 seconds. If it starts, minimize it.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666476.jpg
>* ShowAutomatically = No





### On the Taskbar, open Internet Explorer
On the Taskbar, click the Internet Explorer icon.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773351.jpg
>* ShowAutomatically = No





### Sign in to the Azure Portal
Sign in to the Azure Portal at https://portal.azure.com.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666478.jpg
>* ShowAutomatically = No



#### :calling: COMMAND
```TypeText
https://portal.azure.com
```


### Open Visual Studio solution:
On the taskbar, click the File Explorer icon. Under This PC, go to Allfiles \(F\):\\Mod06\\Labfiles\\Starter\\Contoso.Events, and then double-click Contoso.Events.sln.

#### :bulb: KNOWLEDGE
Note that Known file extensions \(such as .sln\) may be hidden. See screenshot. It may also take a while for Visual Studio to open.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666479.jpg





### Open the TableStorageHelper.cs file
In the Solution Explorer pane, expand the Roles solution folder. In the Solution Explorer pane, expand the Contoso.Events.Worker project. Double-click the TableStorageHelper.cs file.

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666480.jpg





### Find the method with the following signature
In the TableStorageHelper class, find the method with the following signature:  
IEnumerable<string> GetRegistrantNames\(string eventKey\);

#### :bulb: KNOWLEDGE
Use Auto Hide to hide windows using the push-pull pin on each window to allow more room for the script editor.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666481.jpg





### Remove the following single line of code:
Remove the following single line of code in the class:  
return Enumerable.Empty<string>\(\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666482.jpg





### Create a CloudTable instance:
At the end of the GetRegistrantNames method and before the closing brace, create a CloudTable instance:  
CloudTable table = \_tableClient.GetTableReference\("EventRegistrations"\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors. Note that Word Wrap is enabled in Tools/Options/Text Editor/All Languages

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666483.jpg



#### :calling: COMMAND
```TypeText
CloudTable table = _tableClient.GetTableReference("EventRegistrations");
```


### Store the eventKey in a string variable:
At the end of the GetRegistrantsNames method and before the closing brace, store the eventKey in a string variable named partitionKey:  
string partitionKey = eventKey;

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666484.jpg



#### :calling: COMMAND
```TypeText
string partitionKey = eventKey;
```


### Create a string filter:
Create a string filter by using the TableQuery.GenerateFilterCondition, as shown below:  
string filter = TableQuery.GenerateFilterCondition\("PartitionKey", QueryComparisons.Equal, partitionKey\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666485.jpg



#### :calling: COMMAND
```TypeText
string filter = TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, partitionKey);
```


### Create a new instance of the TableQuery class:
At the end of the GetRegistrantsNames method and before the closing brace, create a new instance of the TableQuery class and use the fluent Where method with your filter to generate a query:  
TableQuery<Registration> query = new TableQuery<Registration>\(\).Where\(filter\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666486.jpg



#### :calling: COMMAND
```TypeText
TableQuery<Registration> query = new TableQuery<Registration>().Where(filter);
```


### Pass the generated query into ExecuteQuery method:
Pass the generated query into the ExecuteQuery method of the table variable by using the Registration model class as the generic parameter:  
IEnumerable<Registration> registrations = table.ExecuteQuery<Registration>\(query\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666487.jpg



#### :calling: COMMAND
```TypeText
IEnumerable<Registration> registrations = table.ExecuteQuery<Registration>(query);
```


### Store the registrations in a variable:
At the end of the GetRegistrantsNames method and before the closing brace, add a statement without the closing semi-colon to store the registrations in a variable of the same type named names:  
IEnumerable<string> names = registrations

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666488.jpg



#### :calling: COMMAND
```TypeText
IEnumerable<string> names = registrations
```


### Append the lambda-syntax query:
Append the lambda-syntax query with a fluent method to order the result by LastName:  
.OrderBy\(r => r.LastName\)

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666489.jpg



#### :calling: COMMAND
```TypeText
.OrderBy(r => r.LastName)
```


### Append the query further with a fluent method:
Append the query further with a fluent method to order the result by FirstName:  
.ThenBy\(r => r.FirstName\)

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666490.jpg



#### :calling: COMMAND
```TypeText
.ThenBy(r => r.FirstName)
```


### Finalize the query with a projection method:
Finalize the query with a projection method that uses the String.Format static method to format the string with LastName, followed by a command, then a space, and then the FirstName:  
.Select\(r => String.Format\("\{1\}, \{0\}", r.FirstName, r.LastName\)\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666491.jpg



#### :calling: COMMAND
```TypeText
.Select(r => String.Format("{1}, {0}", r.FirstName, r.LastName));
```


### Return statement:
At the end of the GetRegistrantsNames method and before the closing brace, add the following statement:  
return names;

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666492.jpg



#### :calling: COMMAND
```TypeText
return names;
```



# Exercise 2: Updating the Events Website to use Storage Tables
## INTRODUCTION MESSAGE
In this exercise, you will:  
  
Update the existing Contoso.Events application to use Table storage.  
The main tasks for this exercise are as follows:  
  
Update the register controller action to store the registration record.  
Update the register ViewModel to retrieve the dynamic stub registration from the table.
## COMPLETION MESSAGE
Results: After completing this exercise, you will have used the Azure Storage SDK to retrieve and create entities.
### Update the register controller action:
In the Solution Explorer pane, expand the Roles solution folder. Expand the Contoso.Events.Web project. Expand the Controllers folder. Double-click the RegisterController.cs file.

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666493.jpg
>* ShowAutomatically = No





### Find the method with the following signature:
In the RegisterController class, find the method with the following signature:  
private Guid StoreRegistration\(dynamic registration\)

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666494.jpg





### Remove the single line of code in the class:
Remove the single line of code in the class:  
return Guid.Empty;

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666495.jpg





### Get the connection string
At the end of the StoreRegistration method and before the closing brace, get the connection string by using the ConfigurationManager.AppSettings property and the Microsoft.WindowsAzure.Storage.ConnectionString value as the parameter:  
string connectionString = ConfigurationManager.AppSettings\["Microsoft.WindowsAzure.Storage.ConnectionString"\];

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666496.jpg



#### :calling: COMMAND
```TypeText
string connectionString = ConfigurationManager.AppSettings["Microsoft.WindowsAzure.Storage.ConnectionString"];
```


### Get the storage account:
Use the CloudStorageAccount.Parse static method with the connection string as the parameter to get the storage account:  
var storageAccount = Microsoft.WindowsAzure.Storage.CloudStorageAccount.Parse\(connectionString\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666497.jpg



#### :calling: COMMAND
```TypeText
var storageAccount = Microsoft.WindowsAzure.Storage.CloudStorageAccount.Parse(connectionString);
```


### Create a CloudTableClient variable:
At the end of the StoreRegistration method and before the closing brace, create a CloudTableClient variable by using the CreateCloudTableClient method of the storage account:  
var tableClient = storageAccount.CreateCloudTableClient\(\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666498.jpg



#### :calling: COMMAND
```TypeText
var tableClient = storageAccount.CreateCloudTableClient();
```


### Create a CloudTable variable:
By using the GetTableReference method of the CloudTableClient variable and “EventRegistrations” as the parameter, create a CloudTable variable:  
var table = tableClient.GetTableReference\("EventRegistrations"\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666499.jpg



#### :calling: COMMAND
```TypeText
var table = tableClient.GetTableReference("EventRegistrations");
```


### Create a new TableOperation:
At the end of the StoreRegistration method and before the closing brace, create a new TableOperation by using the TableOperation.Insert static method and the dynamic registration as the parameter:  
var operation = TableOperation.Insert\(registration\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666500.jpg



#### :calling: COMMAND
```TypeText
var operation = TableOperation.Insert(registration);
```


### Invoke the Execute method:
By using the CloudTable variable, invoke the Execute method by passing the TableOperation as the parameter:  
table.Execute\(operation\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666501.jpg



#### :calling: COMMAND
```TypeText
table.Execute(operation);
```


### Parse the registration.RowKey string:
At the end of the StoreRegistration method and before the closing brace, parse the registration.RowKey string as a System.Guid by using the Guid.Parse static method :  
Guid rowKey = Guid.Parse\(registration.RowKey\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666502.jpg



#### :calling: COMMAND
```TypeText
Guid rowKey = Guid.Parse(registration.RowKey);
```


### Return the rowKey variable as the result:
Return the rowKey variable as the result of the StoreRegistration method.  
return rowKey;

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666503.jpg



#### :calling: COMMAND
```TypeText
return rowKey;
```


### Open RegisterViewModel.cs
In the Solution Explorer pane, scroll down and expand the folder named "Shared". Expand the Contoso.Events.ViewModels project. Double-click the RegisterViewModel.cs file.

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666504.jpg





### Locate the method with the following signature:
In the RegisterViewModel class, locate the method with the following signature:  
public RegisterViewModel\(string eventKey\)

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666505.jpg





### Get the connection string:
At the end of the RegisterViewModel constructor and before the closing brace, get the connection string using the ConfigurationManager.AppSettings property and the Microsoft.WindowsAzure.Storage.ConnectionString value as the parameter:  
string connectionString = ConfigurationManager.AppSettings\["Microsoft.WindowsAzure.Storage.ConnectionString"\];

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666506.jpg



#### :calling: COMMAND
```TypeText
string connectionString = ConfigurationManager.AppSettings["Microsoft.WindowsAzure.Storage.ConnectionString"];
```


### Get the storage account:
Use the CloudStorageAccount. Parse static method with the connection string as the parameter to get the storage account:  
var storageAccount = Microsoft.WindowsAzure.Storage.CloudStorageAccount.Parse\(connectionString\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666507.jpg



#### :calling: COMMAND
```TypeText
var storageAccount = Microsoft.WindowsAzure.Storage.CloudStorageAccount.Parse(connectionString);
```


### Create a CloudTableClient variable:
At the end of the RegisterViewModel constructor and before the closing brace, create a CloudTableClient variable by using the CreateCloudTableClient method of the storage account:  
var tableClient = storageAccount.CreateCloudTableClient\(\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666508.jpg



#### :calling: COMMAND
```TypeText
var tableClient = storageAccount.CreateCloudTableClient();
```


### Create a CloudTable variable:
Create a CloudTable variable by using the GetTableReference method of the CloudTableClient variable and “EventRegistrations” as the parameter:  
var table = tableClient.GetTableReference\("EventRegistrations"\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666509.jpg



#### :calling: COMMAND
```TypeText
var table = tableClient.GetTableReference("EventRegistrations");
```


### Store the eventKey in a string variable:
At the end of the RegisterViewModel constructor and before the closing brace, store the eventKey in a string variable named partitionKey:  
string partitionKey = String.Format\("Stub\_\{0\}", this.Event.EventKey\);

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666510.jpg



#### :calling: COMMAND
```TypeText
string partitionKey = String.Format("Stub_{0}", this.Event.EventKey);
```


### Create a string filter:
Create a string filter by using the TableQuery.GenerateFilterCondition  
string filter = TableQuery.GenerateFilterCondition\("PartitionKey", QueryComparisons.Equal, partitionKey\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666511.jpg



#### :calling: COMMAND
```TypeText
string filter = TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, partitionKey);
```


### Create a new instance of the TableQuery class:
At the end of the RegisterViewModel constructor and before the closing brace, create a new instance of the TableQuery class and generate a query by using the fluent Where method with your filter :  
TableQuery query = new TableQuery\(\).Where\(filter\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666512.jpg



#### :calling: COMMAND
```TypeText
TableQuery query = new TableQuery().Where(filter);
```


### Pass the generated query into ExecuteQuery method
Pass the generated query into the ExecuteQuery method of the table variable:  
IEnumerable<DynamicTableEntity> tableEntities = table.ExecuteQuery\(query\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666513.jpg



#### :calling: COMMAND
```TypeText
IEnumerable<DynamicTableEntity> tableEntities = table.ExecuteQuery(query);
```


### Select the single element in the enumerable:
At the end of the RegisterViewModel constructor and before the closing brace, select the single element in the enumerable of DynamicTableEntity objects:  
DynamicTableEntity tableEntity = tableEntities.SingleOrDefault\(\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666514.jpg



#### :calling: COMMAND
```TypeText
DynamicTableEntity tableEntity = tableEntities.SingleOrDefault();
```


### Set the RegistrationStub property:
Set the RegistrationStub property to the DynamicTableEntity variable:  
this.RegistrationStub = DynamicEntity.GenerateDynamicItem\(tableEntity\);

#### :bulb: KNOWLEDGE
Ignore Intellisense errors at this point

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666515.jpg



#### :calling: COMMAND
```TypeText
this.RegistrationStub = DynamicEntity.GenerateDynamicItem(tableEntity);
```



# Exercise 3: Verifying that the Events Website is Using Azure Storage Tables for Registrations
## INTRODUCTION MESSAGE
In this exercise, you will:  
  
Use an Azure Storage account to test storage entities in development.  
Use Visual Studio to debug an application that uses development storage.  
  
The main tasks for this exercise are as follows:  
  
Create a storage account instance.  
Run the data generation console project to populate the Azure storage table with data.  
Use Cloud Explorer in Visual Studio to view table storage registrations.  
Debug the cloud web project to register for the event.  
Use Cloud Explorer in Visual Studio to view the new table storage registration.
## COMPLETION MESSAGE
Results: After completing this exercise, you will have used Visual Studio and the Azure emulators to create a comprehensive development environment for Azure Storage.
### Switch to Internet Explorer and Azure Portal
Switch to Internet Explorer and Azure Portal, which should already be open. If not, then open Internet Explorer and enter https://portal.azure.com and login.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666524.jpg





### Add Storage Account
In the Browse blade that displays, click Storage accounts. In the Storage accounts blade that displays, view your list of storage account instances. At the top of the Storage accounts blade, click the Add button.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666525.jpg





### In the Create storage account blade:
In the Create storage account blade that displays, perform the following steps: a. In the Name box, provide a globally unique value. b. In the Deployment model section, ensure that the Resource manager option is selected. c. In the Account kind list, ensure that the General purpose option is selected. d. In the Performance section, ensure that the Standard option is selected. e. Click on the Replication list and select the Locally-Redundant Storage \(LRS\) option. Do NOT click Create yet.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773401.jpg





### In the Create storage account blade (continued)
In the Create storage account blade scroll down and perform the following steps: f. Leave Storage Service Encryption as Disabled g. In the Location list, select the region closest to your current location. h. In the Resource group section, select the Use existing option. i. In the Resource group section, locate the dialog box and provide the value 20532. j. Ensure that the Pin to dashboard option is selected. k. Click Create.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/779696.jpg





### Locate Access keys
Once the Storage account instance is created, the blade for the new instance will open automatically.  
In the Storage account blade, record the name of your storage account. In the Settings section, select the Access keys option.  
In the Access keys blade, locate a key that you wish to use.

#### :bulb: KNOWLEDGE
Note: you can use any of the keys listed for this lab.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773402.jpg





### View connection string
For the access key you selected, click the Copy button to the right of the Connection String for the key.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773403.jpg





### If prompted, Allow Access
If prompted, click the Allow Access button to allow the clipboard to be used.

#### :bulb: KNOWLEDGE
Note: This connection string will be used in various parts of this lab.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773404.jpg





### Paste to Notepad
Click the Start button and type Notepad then click to open Notepad. Choose Edit/Paste to paste the access key to Notepad. You will use this to copy the key several times. Select the Format/Word Wrap option to see the whole key.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/773433.jpg





### In Visual Studio, open the app.config file
Switch to Visual Studio. In the Solution Explorer pane, expand the Shared folder. Expand the Contoso.Events.Data.Generation project. Locate and open the app.config file in the project.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666530.jpg





### Within app.config file, locate following code:
Within the app.config file, locate the following configuration setting:  
 <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666531.jpg





### Paste your Storage Account's connection string:
Update the setting by replacing the value of the value attribute \(currently UseDevelopmentStorage=true\) with your Storage Account's connection string.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666532.jpg





### Start Debug instance
In the Solution Explorer pane, right-click the Contoso.Events.Data.Generation project, point to Debug, and then click Start New Instance. Wait for debugging to complete \(when the console window closes\). This may take a few minutes.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666533.jpg





### If you get a debug error, click OK and continue:
If you get a debug error "Could not find file", click OK and continue. This is a Visual Studio debug issue that can be ignored.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/779697.jpg





### Open Cloud Explorer
On the View menu, click Cloud Explorer. In the Cloud Explorer pane, under your Azure account \(not local\), locate the Storage Accounts node and click the arrow at the left side to expand the node. If prompted for your account credentials, sign in by using your Microsoft Account. Expand the node for your newly created Storage Account under the Storage Accounts node.

#### :bulb: KNOWLEDGE
If necessary, click the Microsoft Account icon in the Cloud Exporer \(resembles a user\) then select your subscription and click Apply. If prompted, login with your Microsoft Account and password.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666534.jpg





### Expand the Tables node:
Expand the Tables node immediately under your Storage Account's node. Double-click the EventRegistrations table. In the EventRegistrations \[Table\] tab, scroll through the entities.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666535.jpg





### Drill-down into the properties of a single entity
Drill-down into the properties of a single entity by double-clicking on a row. Exit out of the Edit Entity dialog box by clicking the Cancel button. Close the EventRegistrations \[Table\] tab in Visual Studio.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666536.jpg





### Select Multiple startup projects:
In the Solution Explorer pane, scroll-up to the top, right-click the Contoso.Events solution, and then click Properties. Navigate to the Startup Project section located under the Common Properties header. In the Startup Project section, locate and select the Multiple startup projects option.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666537.jpg





### Within the Multiple startup projects table:
Within the Multiple startup projects table, perform the following actions:   
a. Locate the Contoso.Events.Web entry and change it's Action from None to Start. b. Locate the Contoso.Events.Worker entry and change it's Action from None to Start. Click the OK button to close the Property dialog.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666538.jpg





### Open the web.config file
In the Solution Explorer pane, expand the Roles solution folder. Expand the Contoso.Events.Web project. Locate and open the web.config file in the project.

#### :bulb: KNOWLEDGE
You can Auto Hide the Cloud Explorer by clicking the push-pull pin on the window.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666539.jpg





### Locate the following configuration setting:
Within the web.config file, locate the following configuration setting:  
 <add key="Microsoft.WindowsAzure.Storage.ConnectionString" value="UseDevelopmentStorage=true" />

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666540.jpg





### Paste your Storage Account's connection string.
Update the setting by replacing the value of the value attribute \(currently UseDevelopmentStorage=true\) with your Storage Account's connection string.

#### :bulb: KNOWLEDGE
If necessary, return to the Azure Portal or Notepad and copy the connection string again

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666541.jpg





### Locate and open the app.config file in the project
In the Solution Explorer pane, expand the Contoso.Events.Worker project. Locate and open the app.config file in the project.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666542.jpg





### Within the app.config file:
Within the app.config file, locate the following configuration setting:  
 <add name="AzureWebJobsStorage" connectionString="UseDevelopmentStorage=true" />

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666543.jpg





### Paste your Storage Account's connection string:
Update the setting by replacing the value of the connectionString attribute \(currently UseDevelopmentStorage=true\) with your Storage Account's connection string.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666544.jpg





### Locate the following configuration setting:
Within the app.config file, locate the following configuration setting:  
 <add name="AzureWebJobsDashboard" connectionString="UseDevelopmentStorage=true" />

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666545.jpg





### Update the value of the connectionString:
Update the setting by replacing the value of the connectionString attribute \(currently UseDevelopmentStorage=true\) with your Storage Account's connection string.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666546.jpg





### Locate the StorageConnectionString setting:
Within the app.config file, locate the following configuration setting:  
 <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666547.jpg





### Update the setting by pasting the value:
Update the setting by replacing the value of the value attribute \(currently UseDevelopmentStorage=true\) with your Storage Account's connection string.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666548.jpg





### 19.	On the Debug menu, click Start Debugging
On the Debug menu, click Start Debugging

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666549.jpg





### Verify the home page of the web application:
On the home page of the web application, verify that it displays a list of events.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666550.jpg





### Click any of the events in the list and Register
Click any of the events in the list. On the event web page, click Register Now.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666551.jpg





### Fill out all of the fields and Submit:
Fill out all of the fields in the registration form and click Submit.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666552.jpg





### Close the tab displaying the website.
Close the tab displaying the website.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666553.jpg





### Open Visual Studio Cloud Explorer, View Events
On the View menu, click Cloud Explorer. Expand the node for your newly created Storage Account under the Storage Accounts node. Expand the Tables node. Double-click the EventRegistrations table. Click the Refresh button to get the most recent data. In the yellow prompt asking if you would like to download the remaining entities, click "click here". 

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666554.jpg





### Sort entities in a descending order by Timestamp:
Click Timestamp header twice to sort entities in a descending order by their Timestamp. Locate your new entity at the top of the table.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/666557.jpg





### Review code changes
If you wish, you can review the code modules that you updated earlier in the lab. You will notice that the Intellisense errors have been resolved as the appropriate library modules were loaded at build time. For instance, see RegisterController.cs tab. If you closed this tab you can reopen it by performing the following steps:  
In the Solution Explorer pane, expand the Roles solution folder. Expand the Contoso.Events.Web project. Expand the Controllers folder. Double-click the RegisterController.cs file.

#### :camera: SCREENSHOT
>LODSProperties
>* Uri = screens/672212.jpg





### Close Visual Studio
Close Visual Studio





### Close Internet Explorer
Close Internet Explorer





### Close File Explorer
Close File Explorer





### Close Server Manager
Close Server Manager





### Close Notepad, if open
Close Notepad, if open without saving





### Close RDP session
Close RDP session and click OK to disconnect





### Stop VM to save billing charges
If you are stopping labs for the day, on the vm2032 Overview page in the Azure Portal, click Stop to stop billing charges until you start labs again. If prompted, click Yes to stop the VM.





### Close Internet Explorer
Close Internet Explorer to end the lab






