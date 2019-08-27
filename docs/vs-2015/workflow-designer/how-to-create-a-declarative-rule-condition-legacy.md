---
title: 如何：创建声明性规则条件 （旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- declarative rule conditions
- condition statements, declarative rule conditions
- Rule Condition Editor dialog box
ms.assetid: 804b6129-c433-408f-a424-46987967730c
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: dbdcc268b71f2926307b500126840391dd5308fd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62931248"
---
# <a name="how-to-create-a-declarative-rule-condition-legacy"></a>如何：创建声明性规则条件（旧版）
本主题介绍如何使用面向 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 来声明规则条件。  
  
 条件语句的计算结果为 **，则返回 True**或**False**。 声明性规则条件是通过创建一个条件语句[规则条件编辑器对话框 （旧版）](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)和与工作流存储为 XML。 声明性规则条件可以包括一些谓词，这些谓词比较工作流状态和组合多个谓词的布尔代数。  
  
 声明性规则条件用在以下 Windows Workflow Foundation 现成可用的活动中：  
  
- [ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)  
  
- [IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65034)  
  
- [ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)  
  
- [WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)  
  
- [SequentialWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65040)  
  
- [StateMachineWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65045)  
  
### <a name="to-create-a-declarative-rule-condition-using-the-rule-condition-editor"></a>使用规则条件编辑器创建声明性规则条件  
  
1. 在活动的**属性**窗口中，单击**条件**属性或**UntilCondition**属性，具体取决于该活动。  
  
2. 选择**声明性规则条件**从属性列表。  
  
3. 展开**条件**或**UntilCondition**属性。  
  
4. 单击**ConditionName**属性。  
  
5. 单击**ConditionName**省略号 **[...]** 以打开**选择条件**对话框。  
  
6. 单击**新的条件**以打开**规则条件编辑器**对话框。  
  
7. 键入的表达式中的条件**条件**文本框。  
  
     有关如何创建条件表达式的信息，请参阅[规则条件编辑器对话框 （旧版）](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)。  
  
8. 创建的条件表达式完成后，单击**确定**关闭对话框并创建规则条件与分配的名称。  
  
     **选择条件**对话框随即打开。  
  
     有关如何使用信息**选择条件**对话框中，请参阅[选择条件对话框 （旧版）](../workflow-designer/select-condition-dialog-box-legacy.md)。  
  
## <a name="see-also"></a>请参阅  
 [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)   
 [使用 ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65066)   
 [使用 IfElseBranchActivity 活动](http://go.microsoft.com/fwlink?LinkID=65075)   
 [使用 Replicator 活动](http://go.microsoft.com/fwlink?LinkID=65080)   
 [使用 While 活动](http://go.microsoft.com/fwlink?LinkID=65091)   
 [规则条件编辑器对话框 （旧版）](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)   
 [选择条件对话框 （旧版）](../workflow-designer/select-condition-dialog-box-legacy.md)   
 [在工作流中使用条件](http://go.microsoft.com/fwlink?LinkID=65009)