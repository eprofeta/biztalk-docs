---
title: "Monitoring the BizTalk Server Environment | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: baae51cf-0284-429b-8335-bc1ac3e63f4c
caps.latest.revision: 4
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Monitoring the BizTalk Server Environment
You can monitor [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] infrastructure and applications with a manual or automatic process, or a combination of the two methods, using the tools as shown in the following table.  
  
|Manual or Automated Monitoring|Tools|  
|------------------------------------|-----------|  
|Automated Monitoring|-   Microsoft System Center Operations Manager (Operations Manager)|  
|Manual Monitoring|-   The **Group Hub** page in the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console<br />-   Performance Analysis of Logs (PAL) tool<br />-   Event Viewer|  
  
 Whether or not you implement a monitoring application, you should use the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console to monitor the health of your [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] applications and perform root-cause analysis to identify the underlying cause of any problems.  
  
 When monitoring [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)], keep these points in mind:  
  
-   Your infrastructure could be healthy, but your applications might not be (for example, they are receiving invalid messages and are unable to process them).  
  
-   Your infrastructure could be unhealthy, but your applications might be running fine (for example, if a server is down, but there are enough servers assigned to the host to take over the load).  
  
-   An infrastructure problem could surface as an application problem (for example, messages are not being processed fast enough because a server is down).  
  
## Monitoring Types  
 Monitoring your [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] and applications falls into four main categories:  
  
-   Availability monitoring  
  
-   Health monitoring  
  
-   Performance monitoring  
  
-   Threshold monitoring  
  
### Availability Monitoring  
 Availability monitoring answers the question "Is the unavailability of a system or application resource preventing your [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] applications from running optimally?" These issues are almost exclusively system-level, such as availability of services and connections. For example, if an adapter is failing because the Enterprise Single Sign-On service is stopped, this is an availability issue. If one of the servers assigned to a host has failed and your application is falling behind on processing messages, you have an availability issue. Likewise, if an application is stopped and is unable to process messages, you have an availability issue. The following table lists the availability monitoring tools.  
  
|Tool|Task|  
|----------|----------|  
|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console|Check the **Group Hub** page in the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console to see if applications or their components (ports/orchestrations) are stopped.|  
|Operations Manager 2007|The [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] management pack and Operations Manager Operations console displays alerts if critical low-level services such as adapters are unavailable. To effectively monitor [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)], you must monitor non-[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] resources that your applications depend on, such as databases and servers. In addition, you must also install and use the SQL Server, Internet Information Services, and Windows Base Operating System Management Packs. Operations Manager consolidates events of interest from event logs, WMI, and other event providers. For more information about installing all the relevant management packs, see [Checklist: Monitoring BizTalk Server with Operations Manager 2007](../technical-guides/checklist-monitoring-biztalk-server-with-operations-manager-2007.md).|  
|Event Viewer|Look for adapter connection issues, stopped services, and so on.|  
  
### Health Monitoring  
 Health monitoring helps you answer the question, "Are any of my applications or resources in bad health?" For example, are any of my applications or their constituent artifacts currently experiencing exception conditions? Or, are messages suspended because of invalid data in the message payload? The following table shows health-monitoring tools.  
  
|Tool|Task|  
|----------|----------|  
|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console|You use the **Group Hub** page and query pages in the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console to identify application health problems and analyze their cause(s).|  
|Operations Manager|The [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] management pack is your first line of defense to notify you that you have suspended messages and/or service instances in your [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] applications. After receiving notification from Operations Manager, you can transition to the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console to troubleshoot the problem.|  
|Event Viewer|Detect problems that occur during the processing of messages and orchestrations.|  
  
### Performance Monitoring  
 Performance monitoring answers the question, "How efficiently is the system performing its work?" This kind of monitoring focuses primarily on the load on physical resources like databases and disks. For example, if the CPU utilization is consistently at 90 to 100 percent and a backlog of messages is forming, this is a performance issue at the computer level. The following table shows performance-monitoring tools.  
  
|Tool|Task|  
|----------|----------|  
|SQL Query Analyzer|Monitor database size and content to diagnose system problems.|  
|Operations Manager|The [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] management pack and Operations Manager Operations console can be configured to display alerts if critical [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] performance counters such as the Message Box Q size or Host Q size exceed the defined thresholds. To monitor the performance of non-[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] resources that your applications depend on, such as databases and servers, you must also install and use the SQL Server, Internet Information Services, and Windows Base OS Management Packs. For more information about installing all the relevant management packs, see [Checklist: Monitoring BizTalk Server with Operations Manager 2007](../technical-guides/checklist-monitoring-biztalk-server-with-operations-manager-2007.md).<br /><br /> You can also use the Performance Analysis of Logs (PAL) tool to capture the threshold values from the throughput testing to use in the threshold rules in the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] management pack. For more information about the PAL tool, see [Using the Performance Analysis of Logs (PAL) Tool](../technical-guides/using-the-performance-analysis-of-logs-pal-tool.md).|  
|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console|The **Group Hub** page shows key performance metrics such as the number of service instances currently active, dehydrated, ready to run, scheduled, suspended, etc. in your [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] applications.|  
|Business Activity Monitoring (BAM)|You can specify specific stages in your business process for which you want to track key performance indicators pertinent to your business application. Using BAM, you can monitor business metrics as well as IT metrics (for example, SLA's and execution times).|  
  
### Threshold Monitoring  
 Customized threshold rules are an essential element in a mature operations environment. You can create many of these threshold rules in Operations Manager. These threshold rules are typically based on the requirements of the BizTalk application. The Performance Analysis of Logs (PAL) tool can streamline the process of determining the correct values for these thresholds for your environment. The PAL tool comes with some base threshold values that can serve as the core of the data that is used for Microsoft System Center Operations Manager. Implementing those threshold rules in Operations Manager allows for automated monitoring. In addition, an administrator can setup notification rules and can perform actions based on the triggering of a threshold rule (such as running a script, calling .NET code, sending e-mail, etc.). The following table shows threshold-monitoring tools.  
  
|Tool|Task|  
|----------|----------|  
|Performance Analysis of Logs (PAL) tool|The PAL tool automatically reports when performance counters are beyond thresholds. The thresholds dynamically change to be appropriate for the environment of the server. For example, the kernel memory pool thresholds change based on the answers that the user provides about 32-bit/64-bit architecture, amount of physical memory, and /3GB switch. The PAL tool can be downloaded for free at [http://www.codeplex.com/PAL](http://www.codeplex.com/PAL).|  
|Operations Manager|The BizTalk Server management pack and Operation Manager Operations console can be configured to display alerts if critical [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] counters exceed the defined thresholds.|  
  
## Troubleshooting  
 Once you are aware of a health problem with your [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] applications, you can use the **Group Hub** page and **Query** pages in the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console to analyze the problem. The [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administration console provides an integrated configuration, deployment and troubleshooting experience, and you can fix configuration and deployment related problems within the Administration console after you have pinpointed them. Typically, most application problems are due to messages not getting through as expected (this can manifest as suspended service instances, or retrying ports, or dehydrated instances that have not been reactivated, etc.)  
  
 You can use the **Group Hub** page and **Query** pages to group your service instances (whatever state they are in: running, suspended, dehydrated, etc.) by application, error type, service type, host, etc., to isolate the different errors, investigate them one by one, and fix them.