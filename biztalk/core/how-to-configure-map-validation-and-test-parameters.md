---
title: "How to Configure Map Validation and Test Parameters | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1768918c-e94f-476f-b288-9e030c691177
caps.latest.revision: 9
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# How to Configure Map Validation and Test Parameters
Before validating and testing a map, you need to set the map validation and test parameters in the **Properties** window of the map.  
  
## Configure the map validation and test parameters  
  
1.  In Solution Explorer, right-click the map whose property pages you want to configure, and then click **Properties**.  
  
2.  In the Properties window, do the following.  
  
    |Use this|To do this|  
    |--------------|----------------|  
    |**Validate TestMap Input**|Configure whether you want to have the instance message validated against the source schema before you test the map.|  
    |**Validate TestMap Output**|Configure whether you want to have the instance message validated against the destination schema after you test the map.|  
    |**TestMap Input Instance**|Configure the location of the instance message data to use when you test the map.<br /><br /> If you configure this property, you must also configure the **TestMap Input** property.|  
    |**TestMap Output Instance**|Configure the location of the file where you want the output of the test map operation to be stored.<br /><br /> If you configure this property, you must also configure the **TestMap Output** property.|  
    |**TestMap Input**|Configure the input instance data format.|  
    |**TestMap Output**|Configure the output data type to use when you test the map.|  
  
    > [!IMPORTANT]
    >  If you want to test your map, you must configure the map properties first.  

After you have developed your map, one of the next steps is to validate it. This topic provides step-by-step instructions for validating maps.  
  
## Validate a BizTalk map  
  
1.  In Solution Explorer, open the map that you want to validate.  
  
2.  In Solution Explorer, right-click the map, and then select **Validate Map**.  
  
3.  In the **Output** window, verify the results.  
  
> [!IMPORTANT]
>  If you use custom data or constants in your output, you must verify that the data types of your source test data and target constant values are valid. When you validate a map, BizTalk Mapper does not check if the instance data violates any data types defined in the schemas. This is done when you test the map or validate the instance data with BizTalk Editor. 

## Test a BizTalk map

After you have developed your map, one of the next steps is to test it. This topic provides step-by-step instructions for testing maps including steps to view the XSLT generated by the map compiler.  
  
1.  In Solution Explorer, right-click the map you want to test, and then select **Test Map**.  
  
2.  Verify the results in the **Output** window.  
  
    > [!IMPORTANT]
    >  It is recommended that you configure the input and output instance properties in the Properties window before you test a map.  
  
## Review the XSLT  
 It is often useful to inspect the XSLT generated by the map compiler. Some of the benefits of inspecting XSLT include:  
  
-   If you are using looping or custom functoids, you will better understand how the looping is performed and how the custom functoid is invoked.  
  
-   If you have a complicated map, reviewing the XSLT will enable you to see how the map is translated into a transform, and may give you insight on how to better structure, replace, or streamline one or more parts.  
  
-   If you are using custom scripts or other artifacts, reviewing the XSLT will enable you to see how the scripts, artifacts, and other parts of the map interact.  
  
 In other words, reviewing the XSLT is a great way to debug a map.  
  
#### View the XSLT generated by the map compiler  
  
1.  From a Visual Studio BizTalk project, select the **Solution Explorer** tab, right-click a map, and then select **Validate Map**.  
  
2.  Scroll the Output window to find the URL for the XSL file. Press **CTRL**, and select the URL to view the file.  
  
> [!NOTE]
>  Changes made to the XSL file are not reflected in the map and are overwritten on the next build.  
  
## See also  

[How to Debug Maps](../core/how-to-debug-maps.md)  
[Troubleshooting Maps](../core/troubleshooting-maps.md)  