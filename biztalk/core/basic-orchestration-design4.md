---
title: "Basic Orchestration Design4 | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "orchestrations, design"
ms.assetid: 53f90bba-5786-49ca-b4d0-21601ec04045
caps.latest.revision: 7
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Basic Orchestration Design
When you create a basic orchestration, you receive XML in the receive port of your orchestration. The XML is then sent to the back-end system to be processed. In the back-end system, an exception might occur that could stop the orchestration. The exception that is produced provides information that the orchestration was not completed.  
  
 When a fault occurs, the call is suspended. In the Event Viewer log, you can view the fault and the reason for the failure.  
  
 To prevent the orchestration from entering a suspended state and to redirect the fault, you can create a CatchExpression. To trap the exception generated by the back-end, and to help in locating the cause of the problem, you can use the Scope shape in your orchestration.  
  
## See Also  
 [Using BizTalk Server Exception Handling](../core/using-biztalk-server-exception-handling4.md)