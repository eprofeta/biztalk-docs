---
description: "Learn more about: MsSnaStatus_EventTN5250Session Class"
title: "MsSnaStatus_EventTN5250Session Class2 | Microsoft Docs"
ms.custom: ""
ms.date: "11/30/2017"
ms.prod: "host-integration-server"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2c055164-995f-4d79-92a7-e57b82772add
caps.latest.revision: 4
author: "christopherhouser"
ms.author: "hisdocs"
manager: "anneta"
---
# MsSnaStatus_EventTN5250Session Class
The **MsSnaStatus_EventTN5250** class describes a change to the **EventTN5250Session** class.  
  
 The following syntax is simplified from MOF code.  
  
## Syntax  
  
```  
  
class MsSnaStatus_EventTN5250Session: MsSnaStatus_Event  
  
    object ref Path;  
    sint16 Action;  
};  
```  
  
## Remarks  
 **Path**  
 Data Type: **Object ref**Access Type: Read-Only  
  
 The relative path to the corresponding object.  
  
 **Action**  
 Data Type: **sint16** Access Type: Read-Only  
  
 The event that occurred to the object specified in **Path**. The following table describes the valid values for **Action**.  
  
|Value|Description|  
|-----------|-----------------|  
|0|Create|  
|1|Destroy|  
|2|Modify|  
  
## Requirements  
 **Platforms**: Windows Server 2003 R2 SP2, Windows Vista SP2, Windows 7, Windows Server 2008 SP2, Windows Server 2012  
  
## See Also  
 [WmiSnaStatus WMI Provider Classes](../core/wmisnastatus-wmi-provider-classes1.md)   
 [Administration and Management Programmer's Guide](./administration-and-management-programmer-s-guide2.md)
