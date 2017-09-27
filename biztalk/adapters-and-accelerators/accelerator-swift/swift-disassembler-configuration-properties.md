---
title: "SWIFT Disassembler Configuration Properties | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "disassembler, configuration properties"
ms.assetid: 610cc68f-521f-4a9f-9f81-823a2fe55eb1
caps.latest.revision: 3
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# SWIFT Disassembler Configuration Properties
The following table provides SWIFT disassembler (DASM) properties, descriptions, data types, and value ranges.  
  
|Property name|Description|Data type|Value range|  
|-------------------|-----------------|---------------|-----------------|  
|**Batch Header Schema**|Specifies the flat file schema you use for parsing the batch envelope header. Use only if **Inbound Debatching** is set to **True**.|String|None or any deployed schema name|  
|**Batch Trailer Schema**|Specifies the flat file schema to use for parsing the batch envelope trailer. Use only if **Inbound Debatching** is set to **True**.|String|None or any deployed schema name|  
|**BRE Validation**|Enables/disables invocation of Business Rule Engine (BRE) validation. If set to **True**, messages are validated by the BRE against deployed policies (for example, to enforce SWIFT Network Rules). If set to **False**, BRE validation is not invoked.|Boolean|True, False|  
|**Dual Type Message List**|Specifies the SWIFT message types that must inspect a second header field to determine the message sub-type during dynamic message type resolution. The default list is **102 103 521 523 574**. **Note:**  If any or all of the message-type strings are removed from the Dual Type Message List, then for all messages other than MT574, the original schema and its business rules are used in processing the message. For example, an MT102 PLUS instance uses MT102, an MT103PLUS instance uses MT103, an MT521_ISITC instance uses MT521, and an MT523_ISITC instance uses MT523. For all MT574 instances, the following error is returned: Finding document specification by message type "http://schemas.microsoft.com/BizTalk/Solutions/FinancialServices/ SWIFT/Category5/MT574#SWIFT_CATEGORY5_MT574_Interchange" failed. Verify that the schema is deployed properly."|String|Space-separated list of 3-digit numbers|  
|**Fragmentation**|Enables/disables fragmentation of inbound batches. If set to **True**, messages in an inbound batch are published to the MessageBox database as separate messages. If set to **False**, the entire inbound batch is published to the MessageBox database as a single message (as an exact copy of the input). Use only if inbound debatching is set to **True**.|Boolean|True, False|  
|**Inbound Debatching**|Enables/disables processing of inbound batches. If set to **True**, inbound batches are expected and are debatched during processing. If set to **False**, single messages are expected and do not require debatching.|Boolean|True, False|  
|**Message Header Schema**|Specifies the flat file schema to use for parsing the message envelope header (for a message in a batch). Use only if **Inbound Debatching** is set to **True**.|String|None or any deployed schema name|  
|**Message Trailer Schema**|Specifies the flat file schema to use for parsing the message envelope trailer (for a message in a batch). Use only if **Inbound Debatching** is set to **True**.|String|None or any deployed schema name|  
|**Preserve Batch Header**|Enables/disables preservation of batch envelope header when **Fragmentation** is enabled. If set to **True**, the batch envelope header is published to the MessageBox database as a separate message. If set to **False**, the batch envelope header is discarded after it is parsed. Use only if **Batch Header Schema** is specified.|Boolean|True, False|  
|**Preserve Batch Trailer**|Enables/disables preservation of batch envelope trailer when **Fragmentation** is enabled. If set to **True**, the batch envelope trailer is published to the MessageBox database as a separate message. If set to **False**, the batch envelope trailer is discarded after it is parsed. Use only if **Batch Trailer Schema** is specified.|Boolean|True, False|  
|**Preserve Message Header**|Enables/disables preservation of message envelope header (for a message in a batch) when **Fragmentation** is enabled. If set to **True**, the message envelope header is published to the MessageBox database in the header part of the corresponding SWIFT message in the batch. If set to **False**, the message envelope header is discarded after it is parsed. Use only if **Message Header Schema** is specified.|Boolean|True, False|  
|**Preserve Message Trailer**|Enables/disables preservation of message envelope trailer (for a message in a batch) when **Fragmentation** is enabled. If set to **True**, the message envelope trailer is published to the MessageBox database in the trailer part of the corresponding SWIFT message in the batch. If set to **False**, the message envelope trailer is discarded after it is parsed. Use only if **Message Trailer Schema** is specified.|Boolean|True, False|  
|**Preserve Session and Sequence Number**|If set to **True**, preserve any character strings in the session and sequence-number fields in header block 1.<br /><br /> If set to **False**, insert truncated spaces in these fields.|Boolean|True, False|  
|**Promote A4SWIFT SWIFTBound Property**|If set to **True**, promote the **SWIFTBound** property for messages received through this pipeline with a header block 2 (input).<br /><br /> If set to **False**, do not promote the **SWIFTBound** property in any case.|Boolean|True, False|  
|**Suppress Missing Policy Warnings**|Enables/disables logging of Business Rule Engine (BRE) warnings in the Event Log for missing (undeployed) BRE validation policies. If set to **True**, the warnings are suppressed. If set to **False**, a warning is logged every time a validation policy is not found. Use only if **BRE Validation** is enabled.|Boolean|True, False|  
|**SWIFT Header Schema**|Specifies the flat file schema to use for parsing the SWIFT message header and inspecting the parsed values to dynamically discover the message type. Specify only if dynamic message type resolution is required (pipeline will process SWIFT messages of different types). Specify if **SWIFT Interchange Schema** is not specified. If **SWIFT Interchange** and **SWIFT Header Schema** are both unspecified, **SWIFT Header Schema** defaults to **Micrsoft.Solutions.FinancialServices.SWIFT.RuntimeSchemas.HeaderSchema**.|String|None or any deployed schema name|  
|**SWIFT Interchange Schema**|Specifies the flat file schema to use for parsing the entire SWIFT message (interchange). Specify only if dynamic message type resolution is not required (pipeline will only process SWIFT messages of the specified type). Must be specified if **SWIFT Header Schema** is not specified.|String|None or any deployed schema name|  
|**Treat blank lines as parse errors**|If set to **True**, when blank lines are encountered in many multi-line fields, these are flagged as parse errors (blank lines are not good practice according to SWIFT). Note that for debatching scenarios, these parse errors do NOT terminate the batch processing (the message is treated as a message in error and produces an error part), and messages in the batch without errors are properly processed.<br /><br /> If set to **False**, blank lines are allowed in many multi-line fields.|Boolean|True, False|  
|**XML Validation**|Enables/disables invocation of XML validation. If set to **True**, messages are validated by the XML validating reader against schema constraints (for example, to enforce the length or range of a value). If set to **False**, XML validation is not invoked.|Boolean|True, False|  
  
## See Also  
 [Configuring the SWIFT Disassembler](../../adapters-and-accelerators/accelerator-swift/configuring-the-swift-disassembler.md)   
 [Configuring the SWIFT Assembler](../../adapters-and-accelerators/accelerator-swift/configuring-the-swift-assembler.md)