You can try any of the tools based on your requirement to monitor SQL server instances. We have Powerbi that will help you to visualize the collected dataset and take decisions to troubleshoot expensive queries.

SQL_Monitoring by agent jobs
          This tool is limited to working only with Azure Managed Instance and OnPrem SQL instances. It requires the SQL server agent to run certain queries at every 5 second of interval and dump results set in the DBAdmin database. Also, it comes with 7 days of data retention to minimize the database size. To change the data retention period, you can modify the purge job.          
 
 
SQL_Monitoring_by_Powershell
          This is a very comprehensive tool to monitor SQL servers by Powershell commands. It only requires the latest version of PowerShell to work and the destination port should be reachable. It has the following advantages:
       1. Monitor Azure SQL Database, Managed instance, and Onprem SQL server.
       2. Future support for Azure synapse analytics
       3. Visualize data with Powerbi
       4. Fully customizable to add additional scripts to collect data.
       5. Collect performance data either for a single database or all databases.
       6. Monitor performance data on ReadOnly replicas (Onprem/Azure SQL DB/Managed Instances)
       
## Prerequisites
- SQL login that has access to both the user database and master database

 ## To Use
 
1. Unzip SQL_Monitoring_by_Powershell.zip
2. Navigate to the Scripts folder and add target instances in the "InstanceList_DMA_Performance.csv" file.
    Target SQL type: SQLServer , AzureManagedSQLDB , AzureSQLDB , AzureSynapse
   
    e.g File Format >
   
        Environment,Active,InstanceName,DatabaseName,DSNName,Port,AuthType,UserName,Password,QueryTimeout,ConnectionTimeout
        "SQLServer","0","testmachine","master",,,"winint",,,"30","60"
         "AzureManagedSQLDB","1","servername.public.a7b5fb381f7e.database.windows.net","master",,3342,"SQLAuth","Username","Password","30","60"
         "AzureSQLDB","0","servername.database.windows.net","master or any database name",,1433,"SQLAuth","Username","Password","30","60"
         "AzureSynapse","0","servername.database.windows.net","DMAreporting",,1433,"SQLAuth","Username","Password","30","60"
     

2. Open PowerShell and cd to the directory you unzipped the files  (cd C:\SQL_Monitoring_by_Powershell)
 
4. So that you can run the script run and confirm the change
           Set-Executionpolicy -Scope CurrentUser -ExecutionPolicy UnRestricted

5. When an issue occurs, type the following command from PowerShell. This will load all functions in memory.
      . .\SQL_Performance_Data_Capture.ps1
     
6. Run the following command to start data collection:
        Run_SQL_Perf_Collection -PerCollectionTime_In_Min 30 -samplingPeriod_In_Sec 5 -ApplicationIntentReadOnly 0
