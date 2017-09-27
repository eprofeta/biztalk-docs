---
title: "How to Configure the Decide Shape | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Decide shape [Orchestration Designer]"
  - "Decide shape [Orchestration Designer], configuring"
  - "Decide shape [Orchestration Designer], branching"
  - "configuring [Orchestration Designer], Decide shapes"
ms.assetid: 70910861-3834-49e7-ab1e-d62730ea2a95
caps.latest.revision: 6
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# How to Configure the Decide Shape
![](../core/media/ebiz-orch-decide.gif "ebiz_orch_decide")  
Decide shape  
  
 Each branch of a **Decide** shape, except the **else** branch, has a rule associated with it. You can use BizTalk Expression Editor to create a Boolean expression in the rule that is evaluated for the execution of that branch. Because the **else** branch implies the negation of the Boolean expression in the previous branch, it does not have an expression associated with it.  
  
 Below the rule or **else** clause, a branch of a **Decide** shape can contain additional shapes, just like any other part of the orchestration.  
  
### To configure a Decide shape  
  
1.  If BizTalk Expression Editor is not visible, right-click the rule and click **Edit Boolean Expression**, or in the Properties window, click the **Ellipsis** (**...**) button for the **Expression** property.  
  
2.  In BizTalk Expression Editor, create a Boolean expression for each branch except the **Else** branch. For example,  
  
    ```  
    myMessage.Total > 1000  
    myObject.IsValid()  
    myMessage.VIP == true  
    ```  
  
### To add a branch to a Decide shape  
  
1.  Right-click the **Decide** shape, and then click **New Rule Branch**.  
  
     —Or—  
  
2.  Drag a new shape between two existing branches.  
  
    > [!NOTE]
    >  To remove a branch from a **Decide** shape, right-click the branch you want to remove, and then click **Delete**, or select the rule branch and press the **DELETE** key.