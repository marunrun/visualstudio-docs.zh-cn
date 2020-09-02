---
title: 如何：创建声明性规则条件 (旧) |Microsoft Docs
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
ms.openlocfilehash: 0c23fed64d7f3a7681fce96663262f6d633299a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75849337"
---
# <a name="how-to-create-a-declarative-rule-condition-legacy"></a>如何：创建声明性规则条件（旧版）
本主题介绍如何使用面向 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 来声明规则条件。

 Condition 语句的计算结果为 **True** 或 **False**。 声明性规则条件是一个条件语句，该语句通过使用 " [规则条件编辑器" 对话框 (旧) ](../workflow-designer/rule-condition-editor-dialog-box-legacy.md) 创建，并使用工作流以 XML 形式存储。 声明性规则条件可以包括一些谓词，这些谓词比较工作流状态和组合多个谓词的布尔代数。

 声明性规则条件用在以下 Windows Workflow Foundation 现成可用的活动中：

- [ConditionedActivityGroup](https://msdn2.microsoft.com/library/system.workflow.activities.conditionedactivitygroup.aspx)

- [IfElseBranchActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ifelsebranchactivity.aspx)

- [ReplicatorActivity](https://msdn2.microsoft.com/library/system.workflow.activities.replicatoractivity.aspx)

- [WhileActivity](https://msdn2.microsoft.com/library/system.workflow.activities.whileactivity.aspx)

- [SequentialWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequentialworkflowactivity.aspx)

- [StateMachineWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.statemachineworkflowactivity.aspx)

### <a name="to-create-a-declarative-rule-condition-using-the-rule-condition-editor"></a>使用规则条件编辑器创建声明性规则条件

1. 在活动的 " **属性** " 窗口中，单击 " **Condition** " 属性或 " **UntilCondition** " 属性，具体取决于活动。

2. 从属性列表中选择 " **声明性规则条件** "。

3. 展开 **Condition** 或 **UntilCondition** 属性。

4. 单击 " **ConditionName** " 属性。

5. 单击 " **ConditionName** " 省略号 **[...]** 以打开 " **选择条件** " 对话框。

6. 单击 " **新建条件** "，打开 " **规则条件编辑器** " 对话框。

7. 在 " **条件** " 文本框中键入条件的表达式。

     有关如何创建条件表达式的信息，请参阅 " [规则条件编辑器" 对话框 (旧) ](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)。

8. 完成条件表达式的创建后，单击 **"确定"** 以关闭对话框，并创建具有指定名称的规则条件。

     此时将打开 " **选择条件** " 对话框。

     有关如何使用 " **选择条件** " 对话框的信息，请参阅 [ (旧) ](../workflow-designer/select-condition-dialog-box-legacy.md)中的 "选择条件" 对话框。

## <a name="see-also"></a>另请参阅
 使用[ConditionedActivityGroup](https://msdn2.microsoft.com/library/bb675237.aspx)的[旧工作流活动](../workflow-designer/legacy-workflow-activities.md)使用 " [IfElseBranchActivity](https://msdn2.microsoft.com/library/bb628465.aspx) " 活动，在 "[活动](https://msdn2.microsoft.com/library/bb628552.aspx)[规则条件编辑器")  (对话框](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)中使用 "[复制](https://msdn2.microsoft.com/library/bb628544.aspx)器" 活动， [ (旧) ](../workflow-designer/select-condition-dialog-box-legacy.md) [使用工作流中的条件](https://msdn2.microsoft.com/library/bb628447.aspx)
