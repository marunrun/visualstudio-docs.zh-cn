---
title: 如何：创建声明性规则条件（旧版） |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d3a15aad987e46edb58da3560828c70571df2227
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663417"
---
# <a name="how-to-create-a-declarative-rule-condition-legacy"></a>如何：创建声明性规则条件（旧版）
本主题介绍如何使用面向 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 来声明规则条件。

 Condition 语句的计算结果为**True**或**False**。 声明性规则条件是一个条件语句，该语句通过使用 "[规则条件编辑器" 对话框（旧版）](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)创建，并使用工作流以 XML 形式存储。 声明性规则条件可以包括一些谓词，这些谓词比较工作流状态和组合多个谓词的布尔代数。

 声明性规则条件用在以下 Windows Workflow Foundation 现成可用的活动中：

- [ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)

- [IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65034)

- [ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)

- [WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)

- [SequentialWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65040)

- [StateMachineWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65045)

### <a name="to-create-a-declarative-rule-condition-using-the-rule-condition-editor"></a>使用规则条件编辑器创建声明性规则条件

1. 在活动的 "**属性**" 窗口中，单击 " **Condition** " 属性或 " **UntilCondition** " 属性，具体取决于活动。

2. 从属性列表中选择 "**声明性规则条件**"。

3. 展开**Condition**或**UntilCondition**属性。

4. 单击 " **ConditionName** " 属性。

5. 单击 " **ConditionName** " 省略号 **[...]** 以打开 "**选择条件**" 对话框。

6. 单击 "**新建条件**"，打开 "**规则条件编辑器**" 对话框。

7. 在 "**条件**" 文本框中键入条件的表达式。

     有关如何创建条件表达式的信息，请参阅 "[规则条件编辑器" 对话框（旧版）](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)。

8. 完成条件表达式的创建后，单击 **"确定"** 以关闭对话框，并创建具有指定名称的规则条件。

     此时将打开 "**选择条件**" 对话框。

     有关如何使用 "**选择条件**" 对话框的信息，请参阅 "[选择条件" 对话框（旧版）](../workflow-designer/select-condition-dialog-box-legacy.md)。

## <a name="see-also"></a>请参阅
 使用[ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65066)的[旧工作流活动](../workflow-designer/legacy-workflow-activities.md)使用[IfElseBranchActivity 活动](http://go.microsoft.com/fwlink?LinkID=65075)，在 "活动规则条件编辑器["](http://go.microsoft.com/fwlink?LinkID=65091)对话框中使用 "[复制器"](http://go.microsoft.com/fwlink?LinkID=65080)活动[（旧版）](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)[使用工作流中的条件的](http://go.microsoft.com/fwlink?LinkID=65009) ["选择条件" 对话框（旧版）](../workflow-designer/select-condition-dialog-box-legacy.md)