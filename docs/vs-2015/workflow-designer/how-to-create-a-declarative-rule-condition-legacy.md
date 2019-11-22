---
title: 'How to: Create a Declarative Rule Condition (Legacy) | Microsoft Docs'
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
ms.openlocfilehash: 2dc63fc58b22792e566df91bd86cac40e3fd2e65
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297482"
---
# <a name="how-to-create-a-declarative-rule-condition-legacy"></a>如何：创建声明性规则条件（旧版）
本主题介绍如何使用面向 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 来声明规则条件。

 A condition statement evaluates to **True** or **False**. A declarative rule condition is a condition statement that is created by using the [Rule Condition Editor Dialog Box (Legacy)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md) and stored as XML with the workflow. 声明性规则条件可以包括一些谓词，这些谓词比较工作流状态和组合多个谓词的布尔代数。

 声明性规则条件用在以下 Windows Workflow Foundation 现成可用的活动中：

- [ConditionedActivityGroup](https://go.microsoft.com/fwlink?LinkID=65017)

- [IfElseBranchActivity](https://go.microsoft.com/fwlink?LinkID=65034)

- [ReplicatorActivity](https://go.microsoft.com/fwlink?LinkID=65039)

- [WhileActivity](https://go.microsoft.com/fwlink?LinkID=65049)

- [SequentialWorkflowActivity](https://go.microsoft.com/fwlink?LinkID=65040)

- [StateMachineWorkflowActivity](https://go.microsoft.com/fwlink?LinkID=65045)

### <a name="to-create-a-declarative-rule-condition-using-the-rule-condition-editor"></a>使用规则条件编辑器创建声明性规则条件

1. In the activity's **Properties** window, click the **Condition** property or **UntilCondition** property, depending on the activity.

2. Select **Declarative Rule Condition** from the list for the property.

3. Expand the **Condition** or **UntilCondition** property.

4. Click the **ConditionName** property.

5. Click the **ConditionName** ellipses **[…]** to open the **Select Condition** dialog box.

6. Click **New Condition** to open the **Rule Condition Editor** dialog box.

7. Type the expression for the condition in the **Condition** text box.

     For information about how to create condition expressions, see [Rule Condition Editor Dialog Box (Legacy)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md).

8. When you are finished creating the condition expression, click **OK** to close the dialog box and create the rule condition with an assigned name.

     The **Select Condition** dialog box opens.

     For information about how to use the **Select Condition** dialog box, see [Select Condition Dialog Box (Legacy)](../workflow-designer/select-condition-dialog-box-legacy.md).

## <a name="see-also"></a>请参阅
 [Legacy Workflow Activities](../workflow-designer/legacy-workflow-activities.md) [Using the ConditionedActivityGroup](https://go.microsoft.com/fwlink?LinkID=65066) [Using the IfElseBranchActivity Activity](https://go.microsoft.com/fwlink?LinkID=65075) [Using the Replicator Activity](https://go.microsoft.com/fwlink?LinkID=65080) [Using the While Activity](https://go.microsoft.com/fwlink?LinkID=65091) [Rule Condition Editor Dialog Box (Legacy)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md) [Select Condition Dialog Box (Legacy)](../workflow-designer/select-condition-dialog-box-legacy.md) [Using Conditions in Workflows](https://go.microsoft.com/fwlink?LinkID=65009)