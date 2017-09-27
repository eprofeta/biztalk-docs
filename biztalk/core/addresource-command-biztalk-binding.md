---
title: "AddResource Command: BizTalk Binding | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 69c732d3-82c8-4615-b68f-ed29b54ebbf3
caps.latest.revision: 19
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# AddResource Command: BizTalk Binding
To add a binding file to a BizTalk application, you use the **AddResource** command and specify **System.BizTalk:BizTalkBinding** for the **Type** parameter. When you add a binding file, you can specify a deployment environment for it. When you later import the application, you can select this deployment environment to apply the bindings. You can add any number of binding files to a BizTalk application, each one customized for a different deployment environment. You add multiple binding files by running this command for each file to add.  
  
 You can add a binding file that you exported for an assembly, application, or group, as described in [ExportBindings Command](../core/exportbindings-command.md), and then use the AddResource command to add the binding file to an application.  
  
 Running this command adds the binding file to the BizTalk Management database, and the file displays in the Resources folder of the application. In addition, the file is listed when you use the [ListApp Command](../core/listapp-command.md). Unlike importing a binding file, adding a binding file does not immediately change existing bindings. The bindings are not applied until the application is imported into another BizTalk group.  
  
 When you add a binding file, you can specify its deployment environment by using the optional "TargetEnvironment" /Property parameter. The value can be any string that represents the deployment environment in which you want to apply the bindings in this file, such as Test or Production. If you do not specify a value for the /Property parameter, a value of **\<Default>** is automatically specified, and this binding file will be applied each time the application is imported.  
  
 When you import an application that includes one or more binding files that you have explicitly added in this manner, you can select which binding file or files to apply by specifying the value of the /Property parameter. Bindings are applied on application import.  
  
 As bindings are applied during the import process, bindings that have already been applied are overwritten by new bindings that have the same name. In other words, the last binding of a particular name to be applied takes effect. Be aware of this when using multiple binding files. If they contain duplicate entries, the latest applied binding will be in effect. When you import an application, bindings are applied in the following order:  
  
1.  Application bindings generated by BizTalk Server that were not explicitly added to the application via a binding file, but that were explicitly selected by the user for export into the application .msi file.  
  
2.  Binding files that have been explicitly added, and do not have a target deployment environment specified. Bindings in this set are applied in no specific order.  
  
3.  Bindings that have been explicitly added, and that have an associated target deployment environment that matches the deployment environment selected for application import. Bindings in this set are applied in no specific order.  
  
 For more information, see [How to Import a BizTalk Application](../core/how-to-import-a-biztalk-application.md). For background information about using binding files, see [Binding Files and Application Deployment](../core/binding-files-and-application-deployment.md).  
  
## Usage  
 **BTSTask AddResource** [**/ApplicationName:"***value***"**] **/Type:System.BizTalk:BizTalkBinding/Property:TargetEnvironment="***value***"** [**/Overwrite**] **/Source:***value* [**/Server:***value*] [**/Database:***value*]  
  
## Parameters  
  
|Parameter|Required|Value|  
|---------------|--------------|-----------|  
|**/ApplicationName** (or **/A**, see Remarks)|No|Name of the BizTalk application to which to add the binding file. If the name includes spaces, you must enclose it in double quotation marks ("). If the application name is not specified, the default BizTalk application is used.|  
|**/Type** (or **/T**, see Remarks)|Yes|**System.BizTalk:BizTalkBinding** (This value is not case-sensitive.)|  
|**/Source** (or **/So**, see Remarks)|Yes|Full path of the binding file, including the file name. If the path includes spaces, you must enclose it in double quotation marks (").|  
|**/Property:TargetEnvironment=** (or **/P:TargetEnvironment=**, see Remarks)|No|A string that specifies the target deployment environment. You can use any string, for example Production. Example: **/Property:TargetEnvironment="Production"**<br /><br /> If not specified, a value of **\<Default>** is automatically applied. The value is case sensitive. If the value includes spaces, you must enclose it in double quotation marks ("). The maximum length of the environment value is 128 characters.|  
|**/Overwrite** (or **/Ov**, see Remarks)|No|Option to update an existing binding file. If not specified, and the binding file already exists in the application that has the same file name as the file being added, the AddResource operation fails.|  
|**/Server** (or **/Se**, see Remarks)|No|Name of the SQL Server instance hosting the BizTalk Management database, in the form ServerName\InstanceName,Port.<br /><br /> Instance name is only required when the instance name is different than the server name. Port is only required when SQL Server uses a port number other than the default (1433).<br /><br /> Examples:<br /><br /> Server=MyServer<br /><br /> Server=MyServer\MySQLServer,1533<br /><br /> If not provided, the name of the SQL Server instance running on the local computer is used.|  
|**/Database** (or **/Da**, see Remarks)|No|Name of the BizTalk Management database. If not provided, the BizTalk Management database running in the local instance of SQL Server is used.|  
  
## Sample  
 **BTSTask AddResource /ApplicationName:MyApplication /Type:System.BizTalk:BizTalkBinding  /Property:TargetEnvironment=Test /Source:"C:\Binding Files\MyBinding.xml" /Server:MyDatabaseServer /Database:BizTalkMgmtDb**  
  
## Remarks  
 Property names are case-sensitive. Parameters are not case-sensitive. You do not need to type the entire parameter name to specify it; you can type the first few letters of the parameter name that identify it unambiguously.  
  
## See Also  
 [AddResource Command](../core/addresource-command.md)   
 [How to Add a Binding File to an Application](../core/how-to-add-a-binding-file-to-an-application2.md)