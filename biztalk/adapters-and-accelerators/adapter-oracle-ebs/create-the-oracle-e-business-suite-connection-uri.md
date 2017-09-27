---
title: "Create the Oracle E-Business Suite connection URI | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 91eb49fa-2a69-470b-b96d-dc3a6ffafef6
caps.latest.revision: 23
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Create the Oracle E-Business Suite connection URI
The [!INCLUDE[adapteroracleebusinesslong](../../includes/adapteroracleebusinesslong-md.md)] connection URI contains properties that the adapter uses to establish a connection to Oracle E-Business Suite, and essentially the underlying Oracle database. The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] supports two ways of connecting to the underlying Oracle database: using tnsnames.ora and without using tnsnames.ora. Based on the kind of connectivity approach, the format of the connection URI is also different. This topic provides information about the Oracle connection URI and also provides links to other topics that explain how to specify a URI in different programming scenarios.  
  
 Oracle E-Business Suite is an application layer that interfaces with an underlying Oracle database, and is categorized into different applications such as Financials and HR, based on the different needs within an organization. Each of these applications provides various “forms” that enable users to enter data into the underlying Oracle database. Access to these forms is restricted by associating users with an application context that comprises the organization ID to which a user belongs, the  “responsibility” associated with the user, and the name of the Oracle E-Business Suite application that the user wants to invoke. Even though the adapter connects directly to the underlying database and does not use forms to interface with the Oracle E-Business Suite, setting the application context is mandatory when performing operations on the Oracle E-Business Suite artifacts. So, to connect to the Oracle E-Business suite, and the underlying Oracle database, using the [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)], you must:  
  
-   Specify a connection URI to connect to Oracle E-Business Suite and the underlying Oracle database. While establishing a connection, you can choose to specify the credentials for Oracle E-Business Suite or the underlying Oracle database.  
  
-   Set the application context for the user. The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] exposes certain binding properties that accept the credentials and the responsibility. For more information about these binding properties, see [Read about the BizTalk Adapter for Oracle E-Business Suite binding properties](../../adapters-and-accelerators/adapter-oracle-ebs/read-about-the-biztalk-adapter-for-oracle-e-business-suite-binding-properties.md). For more information about setting the application context, see [Set application context](../../adapters-and-accelerators/adapter-oracle-ebs/set-application-context.md).  
  
 This section provides information about how to specify the connection URI to connect to the underlying database using tnsnames.ora and without using tnsnames.ora. It also provides information about using the connection URI to connect to Oracle E-Business Suite.  
  
## Connect using tnsnames.ora  
  
> [!IMPORTANT]
>  -   For this approach, you must add the net service name entry in the tnsnames.ora file on the computer with the adapter client installed. For information about the net service name entry, see [Configure the Oracle client for the E-Business Suite adapter](../../adapters-and-accelerators/adapter-oracle-ebs/configure-the-oracle-client-for-the-e-business-suite-adapter.md).  
> -   Due to an Oracle Client limitation, the **DataSourceName** parameter (net service name) in the connection URI cannot contain more than 39 characters if you are performing operations in a transaction. Therefore, make sure that the value specified for the **DataSourceName** parameter is less than or equal to 39 characters if you will be performing operations in a transaction.  
  
 The connection URI can contain an Oracle net service name that is used to identify the Oracle E-Business Suite service with which you want to connect. The Oracle client resolves the Oracle net service name that you provide in the connection URI to connection information for an Oracle E-Business Suite service, according to a hierarchy of Oracle naming methods that you configure it to use. One common naming method is called local naming. In local naming, the Oracle client uses a file called tnsnames.ora to resolve the Oracle net service name.  
  
 A typical endpoint address URI in [!INCLUDE[nextref_btsWinCommFoundation](../../includes/nextref-btswincommfoundation-md.md)] is represented as: `scheme://userauthparams@hostinfoparams`, where:  
  
-   scheme is the scheme name.  
  
-   userauthparams is a name-value collection of parameters required for user authentication by the endpoint.  
  
-   hostinfoparams is information required to establish the connection to the host; for example, a net service name.  
  
 The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] connection URI adheres to this basic format and is implemented as follows:  
  
```  
oracleebs://User=[USER_NAME];Password=[PASSWORD]@[NET_SERVICE_NAME]  
```  
  
 The following table explains the properties contained in the connection URI.  
  
|Connection URI Property|Category|Description|  
|-----------------------------|--------------|-----------------|  
|[USER_NAME]|userauthparams|The user name to use for authentication. The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] exposes a **ClientCredentialType** binding property that specifies the type of Oracle client credential that the client specifies to establish a connection. The possible values for the **ClientCredentialType** binding property are **Database** and **EBusiness**. Depending on the value for this binding property, you must specify relevant credentials. For more information, see [Oracle Credentials and the Connection URI](#BKMK_OraCreds). **Note:**  You must set the **AcceptCredentialsInUri** binding property to **true** to specify the user name and password in the connection URI. **Note:**  The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] does not preserve the case of the value that you enter for the user name when it connects to Oracle E-Business Suite. The user name is passed to Oracle E-Business Suite using the standard rules of SQL*Plus. However, if you want the case of the user name to be preserved or if you want to enter a user name containing special characters, you must specify the value within double quotes.|  
|[PASSWORD]|userauthparams|The password to use for authentication. The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] exposes a **ClientCredentialType** binding property that specifies the type of Oracle client credential that the client specifies to establish a connection. If the **ClientCredentialType** property is set to **Database**, the clients must specify the password for an Oracle database user. If the **ClientCredentialType** property is set to **EBusiness**, the clients must specify the password for an Oracle E-Business Suite user. **Note:**  The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] does not preserve the case of the value that you enter for the password when it connects to Oracle E-Business Suite. The user name is passed to Oracle E-Business Suite using the standard rules of SQL*Plus. However, if you want the case of the password to be preserved or if you want to enter a password containing special characters, you must specify the value within double quotes.|  
|[NET_SERVICE_NAME]|hostinfoparams|A net service name that is specified in the tnsnames.ora file on the computer where the [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] is installed. For information about net service names and tnsnames.ora, see [Configure the Oracle client for the E-Business Suite adapter](../../adapters-and-accelerators/adapter-oracle-ebs/configure-the-oracle-client-for-the-e-business-suite-adapter.md).|  
  
## Connect without using tnsnames.ora  
  
> [!IMPORTANT]
>  -   For this approach, you need not have the net service name entry in the tnsnames.ora. Also, you do not even need to have the tnsnames.ora file on the computer with the adapter client installed.  
> -   This mode of connectivity is not supported if you are performing operations in a transaction. This is due to a limitation of Oracle Client.  
  
 A typical endpoint address URI in [!INCLUDE[nextref_btsWinCommFoundation](../../includes/nextref-btswincommfoundation-md.md)] is represented as: `scheme://userauthparams@hostinfoparams`, where:  
  
-   scheme is the scheme name.  
  
-   userauthparams is a name-value collection of parameters required for user authentication by the endpoint.  
  
-   hostinfoparams is information required to establish the connection to the host; for example, server name, port number, etc.  
  
 The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] connection URI adheres to this basic format and is implemented as follows:  
  
```  
oracleebs://User=[USER_NAME];Password=[PASSWORD]@[SERVER_NAME]:[PORT_NUMBER]/[SERVICE_NAME]/[SERVICE_TYPE]   
```  
  
 The following table explains the properties contained in the connection URI.  
  
|Connection URI Property|Category|Description|  
|-----------------------------|--------------|-----------------|  
|[USER_NAME]|userauthparams|The user name to use for authentication. The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] exposes a **ClientCredentialType** binding property that specifies the type of Oracle client credential that the client specifies to establish a connection. The possible values for the **ClientCredentialType** binding property are **Database** and **EBusiness**. Depending on the value for this binding property, you must specify relevant credentials. For more information, see [Oracle Credentials and the Connection URI](#BKMK_OraCreds). **Note:**  You must set the **AcceptCredentialsInUri** binding property to **true** to specify the user name and password in the connection URI. **Note:**  The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] does not preserve the case of the value that you enter for the user name when it connects to Oracle E-Business Suite. The user name is passed to Oracle E-Business Suite using the standard rules of SQL*Plus. However, if you want the case of the user name to be preserved or if you want to enter a user name containing special characters, you must specify the value within double quotes.|  
|[PASSWORD]|userauthparams|The password to use for authentication. The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] exposes a **ClientCredentialType** binding property that specifies the type of Oracle client credential that the client specifies to establish a connection. If the **ClientCredentialType** property is set to **Database**, the clients must specify the password for an Oracle database user. If the **ClientCredentialType** property is set to **EBusiness**, the clients must specify the password for an Oracle E-Business Suite user. **Note:**  The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] does not preserve the case of the value that you enter for the password when it connects to Oracle E-Business Suite. The user name is passed to Oracle E-Business Suite using the standard rules of SQL*Plus. However, if you want the case of the password to be preserved or if you want to enter a password containing special characters, you must specify the value within double quotes.|  
|[SERVER_NAME]|hostinfoparams|Name of the server on which the Oracle E-Business Suite is running. This is mandatory.|  
|[PORT_NUMBER]|hostinfoparams|The Oracle Net Listener port. The default value 1521.|  
|[SERVICE_NAME]|hostinfoparams|The Oracle database service name. This is mandatory.|  
|[SERVICE_TYPE]|hostinfoparams|The type of Oracle service. The possible values are **Dedicated** or **Shared**. A dedicated service uses a dedicated server process to serve only one user process. A shared service uses a shared server process that can serve multiple user processes. Default is **Dedicated**.|  
  
##  <a name="BKMK_OraCreds"></a> Oracle Credentials and the Connection URI  
 By default, the [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] throws an exception when the Oracle credentials are specified in the connection URI. This is because these credentials are represented as plain text in the connection URI, and this poses a security risk. You can set the **AcceptCredentialsInUri** binding property to control whether the connection URI can contain credentials for the Oracle database. If the **AcceptCredentialsInUri** property is **false**, which is the default, the [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] throws an exception if the connection URI contains Oracle credentials; if the property is **true**, no exception is thrown.  
  
> [!IMPORTANT]
>  Due to the security risks posed by passing credentials in strings as plain text, you should avoid specifying Oracle database connection credentials in the connection URI. For more information about how to more securely provide credentials for the Oracle database, see [Secure your Oracle EBS applications](../../adapters-and-accelerators/adapter-oracle-ebs/secure-your-oracle-ebs-applications.md).  
  
 You may also choose to specify either the database credentials or the Oracle E-Business Suite credentials for establishing a connection to Oracle E-Business Suite. The adapter exposes three binding properties to enable this behavior: **ClientCredentialType**, **OracleUserName**, **OraclePassword**.  
  
 The possible values for the **ClientCredentialType** binding property are **Database** and **EBusiness**.  
  
-   If the **ClientCredentialType** property is set to **Database**, the clients must specify the database credentials.  
  
-   If the **ClientCredentialType** property is set to **EBusiness**, the clients must specify the Oracle E-Business Suite credentials. In this case, the adapter clients must also specify the database credentials for the **OracleUserName** and **OraclePassword** binding properties.  
  
> [!IMPORTANT]
>  In scenarios where the adapter clients specify the database credentials to connect to Oracle E-Business Suite by setting the **ClientCredentialType** binding property to **Database**, but invoke an Oracle E-Business Suite artifact, the values specified for **OracleUserName** and **OraclePassword** binding properties are used for setting the application context. Setting the application context is mandatory for invoking artifacts in Oracle E-Business Suite. For more information about setting the application context, see [Set application context](../../adapters-and-accelerators/adapter-oracle-ebs/set-application-context.md).  
  
## Using Reserved Characters in the Connection URI  
 The [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] does not support specifying a connection URI that has special characters for any of the parameter values. If the connection parameter values contain special characters, make sure you do one of the following:  
  
-   If you are specifying the URI in [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)] using [!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)] or [!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)], you must specify them as-is in the **URI Properties** tab, that is, without using any escape characters. If you specify the URI directly in the **Configure a URI** field and the connection parameters contain reserved characters, you must specify the connection parameters using proper escape characters.  
  
-   If you are specifying the URI while creating a send or receive port in [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] Administration console, and the connection parameters contain reserved characters, you must specify the connection parameters using proper escape characters.  
  
## Using the Connection URI to Connect to Oracle E-Business Suite  
 The following is an example of a connection URI for [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] using tnsnames.ora.  
  
```  
oracleebs://ADAPTER  
```  
  
 In this example, ADAPTER is a net service name that is associated with the SERVICE NAME and connection information for the target Oracle database in tnsnames.ora.  
  
 The following is an example of a connection URI for [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] without using tnsnames.ora.  
  
```  
oracleebs://yourOracleServer:1521/yourOracleDatabaseServiceName/Dedicated  
```  
  
 In this example, the server name is “yourOracleServer” and the service name is “yourOracleDatabaseServiceName”.  
  
 For information about how to establish a connection to Oracle E-Business Suite when you:  
  
-   Use the [!INCLUDE[consumeadapterservlong](../../includes/consumeadapterservlong-md.md)] or the [!INCLUDE[addadapterservreflong](../../includes/addadapterservreflong-md.md)], see [Connect to the Oracle E-Business Suite in Visual Studio](../../adapters-and-accelerators/adapter-oracle-ebs/connect-to-the-oracle-e-business-suite-in-visual-studio.md).  
  
-   Configure a send port or receive port (location) in a [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] solution, see [Manually configure a physical port binding to the Oracle E-Business adapter](../../adapters-and-accelerators/adapter-oracle-ebs/manually-configure-a-physical-port-binding-to-the-oracle-e-business-adapter.md).  
  
## See Also  
 [Configure the Oracle client for the E-Business Suite adapter](../../adapters-and-accelerators/adapter-oracle-ebs/configure-the-oracle-client-for-the-e-business-suite-adapter.md)   
 [Connect to Oracle E-Business Suite using Windows Authentication](../../adapters-and-accelerators/adapter-oracle-ebs/connect-to-oracle-e-business-suite-using-windows-authentication.md)  
 [Create a connection to Oracle E-Business Suite](../../adapters-and-accelerators/adapter-oracle-ebs/create-a-connection-to-oracle-e-business-suite.md)