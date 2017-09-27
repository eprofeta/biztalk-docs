---
title: "Microsoft.BizTalk.GlobalPropertySchemas Reference | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2acf3083-a0a9-483f-88bf-8023d9933e1e
caps.latest.revision: 12
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Microsoft.BizTalk.GlobalPropertySchemas Reference
The **Microsoft.BizTalk.GlobalPropertySchemas** namespace contains property schemas for the properties that various BizTalk Server components use. This namespace contains system properties that the BizTalk engine uses, transport specific properties that each transport uses for handling the configuration, and properties for configuring pipeline components.  

## Namespace schemas  

 The following table shows the global property schemas included in the **Microsoft.BizTalk.GlobalPropertySchemas** namespace.  
  
|Property schema|Feature area and description|  
|---------------------|----------------------------------|  
|bts-btf2-properties.xsd|Property schema.|  
|btf2-endpoints-header.xsd<br /><br /> btf2-envelope.xsd<br /><br /> btf2-manifest-header.xsd<br /><br /> btf2-process-header.xsd<br /><br /> btf2-properties-header.xsd<br /><br /> btf2-receipt-header.xsd<br /><br /> btf2-services-header.xsd|Schemas that define the BizTalk Framework constructs. These schemas are specific to BizTalk Framework Assembler and Disassembler pipeline components.|  
|bts-system-properties.xsd|This is a system property schema. The BizTalk engine uses most properties in this schema. You can use some properties for message routing. For more information on the properties that you can use for message routing, see **Message Context Properties** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)].|  
|bts-endpoint-properties.xsd|This is an internal property schema.|  
|bts-mime-properties.xsd<br /><br /> bts-xmlnorm-properties.xsd|These are property schemas for pipeline components: MIME, XML, Flat File, and BizTalk Framework Assembler and Disassembler pipeline components.|  
|bts-legacy-properties.xsd|BizTalk uses this schema for upgrading [!INCLUDE[btsBizTalkServer2002](../includes/btsbiztalkserver2002-md.md)] applications to [!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)] applications.|  
|bts-messagetracking-properties.xsd|The tracking engine uses this schema.|  
|bts-file-properties.xsd<br /><br /> bts-ftp-properties.xsd<br /><br /> bts-http-properties.xsd<br /><br /> bts-pop3-properties.xsd<br /><br /> bts-smtp-properties.xsd<br /><br /> soap-encoding_1__1.xsd<br /><br /> soap-envelope_1__1.xsd<br /><br /> bts-soap-properties.xsd<br /><br /> bts-WindowsSharePointServices-properties.xsd|These are transport-specific property schemas. Transports use these schemas to carry specific transport information and configurations. For more information on transports, see [Using Adapters](../core/using-adapters.md).|  
|XLANGsBizTalkProperties.xsd|The orchestration engine uses this schema.|  
  
## See Also  
 [About BizTalk Namespace References Included in BizTalk Projects](../core/about-biztalk-namespace-references-included-in-biztalk-projects.md)