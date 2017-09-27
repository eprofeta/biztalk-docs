---
title: "Insert, update, delete, or select operations on interface tables and views using the WCF service model | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae613c0e-4d9a-4c66-99e4-dd0443f1d495
caps.latest.revision: 9
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Insert, update, delete, or select operations on interface tables and views using the WCF service model
The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] discovers a set of basic Insert, Select, Update, and Delete operations on interface tables. By using these operations, you can perform simple Insert, Select, Update, and Delete statements qualified by a WHERE clause on a target interface table. This topic provides instructions on how to perform these operations using the WCF service model.  
  
> [!NOTE]
>  The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] supports only Select operations on interface views.  
  
 For more information about how the adapter supports these operations, see [Operations on Interface Tables and Interface Views](../../adapters-and-accelerators/adapter-oracle-ebs/operations-on-interface-tables-and-interface-views.md).  
  
## About the Examples Used in this Topic  
 The example in this topic performs operations on the MS_SAMPLE_EMPLOYEE interface table. The table is created by running the script provided with the samples. For more information about samples, see [Samples for the Oracle EBS adapter](../../adapters-and-accelerators/adapter-oracle-ebs/samples-for-the-oracle-ebs-adapter.md). A sample, **Interface_Table_Ops**, which is based on this topic, is also provided with the [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] samples.  
  
## The WCF Client Class  
 The name of the WCF client generated for the basic operations that the [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] discovers is based on the name of the table or view, as listed in the following table.  
  
|Artifact|WCF Client Name|  
|--------------|---------------------|  
|Interface tables|InterfaceTables_[APP_NAME]_[SCHEMA]\_[TABLE_NAME]Client|  
|Interface views|InterfaceViews_[APP_NAME]_[SCHEMA]\_[VIEW_NAME]Client|  
  
 [APP_NAME] = Actual name of the Oracle E-Business Suite application; for example, FND.  
  
 [SCHEMA] = Collection of artifacts; for example, APPS.  
  
 [TABLE_NAME] = The name of the table; for example, MS_SAMPLE_EMPLOYEE.  
  
 [VIEW_NAME] = The name of the view; for example, MS_SAMPLE_EMPLOYEE_View.  
  
### Method Signature for Invoking Operations on Tables  
 The following table shows the method signatures for the basic operations on an table. The signatures are the same for a view, except that the view namespace and name replace those of the table.  
  
|Operation|Method Signature|  
|---------------|----------------------|  
|Insert|string Insert(InsertRecord[] RECORDSET);|  
|Select|SelectRecord[] Select(string COLUMN_NAMES, string FILTER);|  
|Update|string Update(UpdateRecord RECORDSET, string FILTER);|  
|Delete|string Delete(string FILTER);|  
  
 As an example, the following code shows the method signatures for a WCF client class generated for the Delete, Insert, Select and Update operations on the MS_SAMPLE_EMPLOYEE interface table under the default APPS schema.  
  
```  
public partial class InterfaceTables_FND_APPS_MS_SAMPLE_EMPLOYEEClient : System.ServiceModel.ClientBase<InterfaceTables_FND_APPS_MS_SAMPLE_EMPLOYEE>, InterfaceTables_FND_APPS_MS_SAMPLE_EMPLOYEE {      
    public SelectRecord[] Select(string COLUMN_NAMES, string FILTER);  
  
    public string Insert(InsertRecord[] RECORDSET);  
  
    public string Update(UpdateRecord RECORDSET, string FILTER);  
  
    public string Delete(string FILTER);  
}  
```  
  
 In this snippet, **InterfaceTables_FND_APPS_MS_SAMPLE_EMPLOYEEClient** is the name of the WCF class in the OracleEBSBindingClient.cs generated by the [!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)].  
  
### Parameters for Table Operations  
 This section provides the parameters required by each table operation  
  
 **Select Operation**  
  
|COLUMN_NAMES|FILTER|  
|-------------------|------------|  
|A comma-delimited list of column names in the target; for example, "EMP_NO, DESIGNATION". The column list specifies the columns of the target that should be returned in the result set. Columns not specified in the column list will be set to their .NET default values in the returned record set. For nillable columns, this value is **null**.|The contents of a WHERE clause that specifies the target rows of the query; for example, "Designation = 'Manager'". You can set this parameter to **null** to return all rows of the target.|  
  
 The return value for a Select operation is a strongly-typed result set that contains the specified columns and rows.  
  
 **Insert Operation**  
  
|Insert operation type|RECORDSET|  
|---------------------------|---------------|  
|Multiple record|A collection of INSERTRECORDS that should be inserted into the table.|  
  
 The return value for an Insert operation is the number of rows inserted.  
  
 **Update Operation**  
  
|RECORDSET|FILTER|  
|---------------|------------|  
|A collection of records that should be updated in the table.|The contents of a WHERE clause that specifies the target rows of the query; for example, "Designation = 'Manager'". You can set this parameter to **null** to return all rows of the target.|  
  
 The return value for an Update operation is the number of rows updated.  
  
 **Delete Operation**  
  
 The Delete operation takes as input a WHERE clause that specifies the rows to be deleted. The return value for a Delete operation is the number of rows deleted.  
  
## Creating a WCF Client to Invoke Operations on Interface Tables and Interface Views  
 The generic set of actions required to perform an operation on Oracle E-Business Suite using a WCF client involves a set of tasks described in [Overview of the WCF channel model with the Oracle E-Business Suite adapter](../../adapters-and-accelerators/adapter-oracle-ebs/overview-of-the-wcf-channel-model-with-the-oracle-e-business-suite-adapter.md). This section describes how to create a WCF client to invoke basic Insert, Select, Update, Delete operations on an interface table.  
  
#### To create a WCF client to perform operations on tables  
  
1.  Create a Visual C# project in Visual Studio. For this topic, create a console application.  
  
2.  Generate the WCF client class for the Insert, Select, Update, and Delete operation on the MS_SAMPLE_EMPLOYEE interface table. For more information about generating a WCF client class, see [Generate a WCF client or a WCF service contract for Oracle E-Business Suite solution artifacts](../../adapters-and-accelerators/adapter-oracle-ebs/create-a-wcf-client-or-wcf-service-contract-for-oracle-ebs-solution-artifacts.md).  
  
    > [!IMPORTANT]
    >  Before generating the WCF client class, make sure you set the **EnableBizTalkCompatibilityMode** binding property to false.  
  
3.  In the Solution Explorer, add reference to `Microsoft.Adapters.OracleEBS` and `Microsoft.ServiceModel.Channels`.  
  
4.  Open the Program.cs file and add the following namespaces:  
  
    -   `Microsoft.Adapters.OracleEBS`  
  
    -   `System.ServiceModel`  
  
5.  Open the Program.cs file and create a client as described in the snippet below.  
  
    ```  
    OracleEBSBinding binding = new OracleEBSBinding();  
    EndpointAddress address = new EndpointAddress("oracleebs://ebs_instance_name");  
    InterfaceTables_FND_APPS_MS_SAMPLE_EMPLOYEEClient client = new InterfaceTables_FND_APPS_MS_SAMPLE_EMPLOYEEClient(binding, address);  
    ```  
  
     In this snippet, `InterfaceTables_FND_APPS_MS_SAMPLE_EMPLOYEEClient` is the WCF client defined in OracleEBSBindingClient.cs. This file is generated by the [!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)].  
  
    > [!NOTE]
    >  In this snippet, you explicitly specify the binding and endpoint address in your application code. You can use these values from the application configuration file, app.config, also generated by the [!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]. For more information on the different ways of specifying client binding, see [Configure a client binding for the Oracle E-Business Suite](../../adapters-and-accelerators/adapter-oracle-ebs/configure-a-client-binding-for-the-oracle-e-business-suite.md).  
  
6.  Set the credentials for the client.  
  
    ```  
    client.ClientCredentials.UserName.UserName = "myuser";  
    client.ClientCredentials.UserName.Password = "mypassword";  
    ```  
  
7.  Because you are performing an operation on an interface table, you must set the application context. In this example, to set the application context, you specify the **OracleUserName**, **OraclePassword**, and **OracleEBSResponsibilityName** binding properties. For more information about application context, see [Set application context](../../adapters-and-accelerators/adapter-oracle-ebs/set-application-context.md).  
  
    ```  
    binding.OracleUserName = "myOracleEBSUserName";  
    binding.OraclePassword = "myOracleEBSPassword";  
    binding.OracleEBSResponsibilityName = "myOracleEBSResponsibility";  
    ```  
  
8.  Open the client as described in the snippet below:  
  
    ```  
    try  
    {  
       Console.WriteLine("Opening Client...");  
       client.Open();  
    }  
    catch (Exception ex)  
    {  
       Console.WriteLine("Exception: " + ex.Message);  
       throw;  
    }  
    ```  
  
9. Invoke the Insert operation on the MS_SAMPLE_EMPLOYEE table.  
  
    ```  
    Console.WriteLine("The application will insert a record in the MS_SAMPLE_EMPLOYEE interface table");  
  
    // The date values cannot contain time zone information. Hence, you must use  
    // DateTimeKind.Unspecified to not include the time zone information.  
    DateTime date = new DateTime(DateTime.Now.Ticks, DateTimeKind.Unspecified);  
  
    string result;  
  
    InsertRecord[] recordSet = new InsertRecord[1];  
  
    EMP_NO__COMPLEX_TYPE emp_no = new EMP_NO__COMPLEX_TYPE();  
    emp_no.Value = "10007";  
  
    NAME__COMPLEX_TYPE name = new NAME__COMPLEX_TYPE();  
    name.Value = "John Smith";  
  
    DESIGNATION__COMPLEX_TYPE desig = new DESIGNATION__COMPLEX_TYPE();  
    desig.Value = "Manager";  
  
    SALARY__COMPLEX_TYPE salary = new SALARY__COMPLEX_TYPE();  
    salary.Value = "500000";  
  
    JOIN_DATE__COMPLEX_TYPE doj = new JOIN_DATE__COMPLEX_TYPE();  
    doj.Value = date;  
  
    recordSet[0] = new InsertRecord();  
    recordSet[0].EMP_NO = emp_no;  
    recordSet[0].NAME = name;  
    recordSet[0].DESIGNATION = desig;  
    recordSet[0].SALARY = salary;  
    recordSet[0].JOIN_DATE = doj;  
  
    try  
    {  
       result = client.Insert(recordSet);   
    }  
    catch (Exception ex)  
    {  
       Console.WriteLine("Exception: " + ex.Message);  
       throw;  
    }  
  
    Console.WriteLine("Number of records inserted= " + result);  
    Console.WriteLine("Press any key to continue...");  
    Console.ReadLine();  
  
    ```  
  
     You can replace the preceding code snippet to perform Select, Update, or Delete operations as well. You can also append the code snippets to perform all operation in a single application. For code snippets on how to perform these operations, see [Select Operation](#BKMK_Select), [Update Operation](#BKMK_Update), and [Delete Operation](#BKMK_Delete) respectively.  
  
10. Close the client as described in the snippet below:  
  
    ```  
    client.Close();  
    Console.WriteLine("Press any key to exit...");  
    Console.ReadLine();  
    ```  
  
11. Build the project and then run it. The application inserts a record in the MS_SAMPLE_EMPLOYEE table.  
  
###  <a name="BKMK_Select"></a> Select Operation  
 The following code shows a Select operation that targets the MS_SAMPLE_EMPLOYEE interface table. The Select operation selects the last record inserted into the table. The returned record is written to the console.  
  
```  
Console.WriteLine("The application will now select the last inserted record");  
SelectRecord[] selectRecords;  
try  
{  
   selectRecords = client.Select("*", "WHERE EMP_NO LIKE 10007");  
}  
catch (Exception ex)  
{  
   Console.WriteLine("Exception: " + ex.Message);  
   throw;  
}  
  
Console.WriteLine("The details of the newly added employee are:");  
Console.WriteLine("********************************************");  
for (int i = 0; i < selectRecords.Length; i++)  
{  
   Console.WriteLine("Employee ID         : " + selectRecords[i].EMP_NO);  
   Console.WriteLine("Employee Name       : " + selectRecords[i].NAME);  
   Console.WriteLine("Employee Desigation : " + selectRecords[i].DESIGNATION);  
   Console.WriteLine("Employee Salary     : " + selectRecords[i].SALARY);  
   Console.WriteLine();  
}  
Console.WriteLine("********************************************");  
Console.WriteLine("Press any key to continue ...");  
Console.ReadLine();  
```  
  
###  <a name="BKMK_Update"></a> Update Operation  
 The following code shows an Update operation that targets the MS_SAMPLE_EMPLOYEE interface table.  
  
```  
Console.WriteLine("The application will now update the employee name in the newly inserted record");  
string recordsUpdated;  
UpdateRecord updateRecordSet = new UpdateRecord();  
updateRecordSet.NAME = "Tom Smith";  
updateRecordSet.DESIGNATION = "Accountant";  
  
try  
{  
   recordsUpdated = client.Update(updateRecordSet, "WHERE EMP_NO LIKE 10007");  
}  
catch (Exception ex)  
{  
   Console.WriteLine("Exception: " + ex.Message);  
   throw;  
}  
  
Console.WriteLine("No of records updated: " + recordsUpdated);  
Console.WriteLine("Press any key to continue...");  
Console.ReadLine();  
```  
  
###  <a name="BKMK_Delete"></a> Delete Operation  
 The following code shows a Delete operation that targets the MS_SAMPLE_EMPLOYEE interface table.  
  
```  
Console.WriteLine("The sample will now delete the record that it first inserted");  
string deletedRecords;  
try  
{  
   deletedRecords = client.Delete("WHERE EMP_NO LIKE 10007");  
}  
catch (Exception ex)  
{  
   Console.WriteLine("Exception: " + ex.Message);  
   throw;  
}  
Console.WriteLine("No of records deleted: " + deletedRecords);  
Console.WriteLine("Press any key to exit...");  
Console.ReadLine();  
```  
  
## See Also  
 [Develop Oracle E-Business Suite applications using the WCF Service Model](../../adapters-and-accelerators/adapter-oracle-ebs/develop-oracle-e-business-suite-applications-using-the-wcf-service-model.md)