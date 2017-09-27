---
title: "Exception Management Framework | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b5aebc0-2467-4f48-a385-056507ed1c1e
caps.latest.revision: 5
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Exception Management Framework
The ESB Exception Management Framework provides a unified message-oriented fault generation mechanism for managing all exceptions that may occur within a [!INCLUDE[prague](../includes/prague-md.md)] environment. The ESB Exception Management Framework can receive exception messages published through the Exception Publishing Service, in addition to messages from the BizTalk Server Failed Message Routing mechanism.  
  
 The framework provides an API for fault message creation, publication, and management from orchestration processes, replicating the BizTalk Server failed message routing feature first introduced with BizTalk Server 2006. In addition, the framework provides facilities for normalizing all exceptions, enriching them, applying Business Activity Monitoring (BAM) tracking, and publishing the final output to the Exception Management database for display and reporting in the ESB Management Portal.  
  
 The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] includes the following pipeline components that support the ESB Exception Management Framework:  
  
-   **Exception Fault processor pipeline component.**This component is included as part of the pipeline associated with the ESB Exception Off-ramp. This off-ramp subscribes to all ESB-generated fault messages, in addition to exceptions generated by the BizTalk Server failed message routing mechanism. The component routes fault messages to the ESB exception management ESB Management Portal database, or it can be configured to route to another location. The pipeline component also enriches all fault messages and exceptions with metadata and normalizes them to a common format.  
  
-   **BAM Tracking pipeline component.**This component intercepts and records exception information within the BizTalk Server BAM subsystem and is used exclusively by the Exception Fault Processor pipeline within the Exception Management Framework. Provided with [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] is a sample that demonstrates using BAM as an optional tracking facility for exception information.  
  
 For more information about the Exception Management Framework, see [Using ESB Exception Management](../esb-toolkit/using-esb-exception-management.md).