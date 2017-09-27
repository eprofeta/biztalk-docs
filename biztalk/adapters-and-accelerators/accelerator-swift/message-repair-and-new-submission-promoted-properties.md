---
title: "Message Repair and New Submission Promoted Properties | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "promoted properties, Message Repair and New Submission"
  - "Message Repair and New Submission, promoted properties"
ms.assetid: e980c905-d07f-4fc2-89ca-05e597410733
caps.latest.revision: 3
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Message Repair and New Submission Promoted Properties
The [!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)] Message Repair and New Submission reconciliation includes the following promoted properties.  
  
|Promoted name|Description|Data type|Value range|Usage example|  
|-------------------|-----------------|---------------|-----------------|-------------------|  
|**BTS.Operations**|Indicates the state of [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] processing. Can be one of the following:<br /><br /> **A4SWIFT_MrsrCompleted** indicates that the message repair and new submission process succeeded.<br /><br /> **A4SWIFT_MrsrFailed** indicates that the message repair and new submission process failed.<br /><br /> **A4SWIFT_MrsrUnparsedFailed** indicates that the repair of an unparsed message failed.<br /><br /> **A4SWIFT_MrsrUnparsedComplete** indicates that the repair of an unparsed message succeeded.<br /><br /> **A4SWIFT_DasmMarkedAsFailed** indicates that the message failed processing in the disassembler stage of the receive pipeline.|String|-   A4SWIFT_MrsrCompleted<br />-   A4SWIFT_MrsrFailed<br />-   A4SWIFT_MrsrUnparsedFailed<br />-   A4SWIFT_MrsrUnparsedCompleted<br />-   A4SWIFT_DasmMarkedAsFailed|When the MrsrRepair orchestration receives a repaired unparsed message after the repair, it sets the **BTS.Operation** property to "A4SWIFT_MRSRCompleted" and the **A4SWIFT_Failed** property to False, and then routes the message to the MessageBox. These properties ensure that the repaired unparsed message does not enter the message repair process again.|  
|**Microsoft.Solutions.A4SWIFT. Property.A4SWIFT_Failed**|Indicates whether [!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)] successfully or unsuccessfully processed the message.|Boolean|True, False|Used by the MrsrRepair orchestration to subscribe only to messages from the MessageBox that have failed validation.|  
|**Microsoft.Solutions.A4SWIFT. Property.A4SWIFT_SwiftBound**|Indicates whether the message is bound for the SWIFT network.|Boolean|True, False|Used by the MrsrRepair orchestration to subscribe only to messages from the MessageBox that are bound for the SWIFT network.|  
|**Microsoft.Solutions.A4SWIFT. MRSRProperty.A4SWIFT_MRSRIsNewSubmission**|Indicates whether the message being processed is a new submission.|Boolean|True, False|Used by the MrsrRepair orchestration to indicate that a message has been created in the Create stage of the workflow.|  
|**Microsoft.Solutions.A4SWIFT. MRSRProperty.A4SWIFT_MRSRLastStage**|Indicates the last stage in the repair workflow that succeeded.|String|-|One of the stages defined for a department workflow. Can be a create, repair, rekey-verify, or approval stage.|  
|**Microsoft.Solutions.A4SWIFT. MRSRProperty.A4SWIFT_ MRSRDepartment**|Indicates the department that is being used in the message repair and new submission, as specified by the MrsrDepartmentPolicy BRE policy.|String|-|Set in the [!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)] Administration Console.|  
|**Microsoft.Solutions.A4SWIFT. MRSRProperty.A4SWIFT_ MRSRFailedReason**|Indicates why the message repair and new submission process failed. Can be one of the following:<br /><br /> Rejected indicates that the user rejected the message from within the [!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)] form.<br /><br /> InvalidDigitalSignature indicates that the user's certificate is invalid.<br /><br /> Timeout indicates that the MRSROrchestration timeout value has been reached.<br /><br /> InvalidWorkFlow indicates that the workflow defined for a department is invalid.<br /><br /> CantRepairIn[!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)] indicates that the incoming XML message could not be opened in [!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)].<br /><br /> General Exception|String|-   Rejected<br />-   InvalidDigitalSignature<br />-   Timeout<br />-   InvalidWorkFlow<br />-   General Exception<br />-   CantRepairIn[!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)]|Set by the Message Repair and New Submission orchestration after the process has failed.|  
  
## See Also  
 [A4SWIFT_* Promoted Properties](../../adapters-and-accelerators/accelerator-swift/a4swift-promoted-properties.md)   
 [FIN Response Reconciliation Promoted Properties](../../adapters-and-accelerators/accelerator-swift/fin-response-reconciliation-promoted-properties.md)