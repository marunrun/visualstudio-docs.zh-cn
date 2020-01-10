---
title: "\"规则条件编辑器\" 对话框（旧版） |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Rules.Design.RuleConditionDialog.UI
helpviewer_keywords:
- Rule Condition dialog box
ms.assetid: c7ca8be9-de31-4a64-939c-4d53a50d5e29
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 00df917b05f5073634b0956a0b44e5b0fc6026a6
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846335"
---
# <a name="rule-condition-editor-dialog-box-legacy"></a>“规则条件编辑器”对话框（旧版）
本主题介绍如何使用旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)]中的 "**规则条件编辑器**" 对话框。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 您可以使用 "**规则条件编辑器**" 对话框创建和修改声明性规则条件。 这些规则条件作为以下 Windows Workflow Foundation 现成可用的活动属性被公开：

- [ConditionedActivityGroup](https://msdn2.microsoft.com/library/system.workflow.activities.conditionedactivitygroup.aspx)

- [IfElseBranchActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ifelsebranchactivity.aspx)

- [ReplicatorActivity](https://msdn2.microsoft.com/library/system.workflow.activities.replicatoractivity.aspx)

- [WhileActivity](https://msdn2.microsoft.com/library/system.workflow.activities.whileactivity.aspx)

- [SequentialWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequentialworkflowactivity.aspx)

- [StateMachineWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.statemachineworkflowactivity.aspx)

  您可以通过使用 "[选择条件" 对话框（旧版）](../workflow-designer/select-condition-dialog-box-legacy.md)访问 "**规则条件编辑器**" 对话框。

  下表描述了 "**规则条件编辑器**" 对话框的用户界面（UI）元素。

|UI 元素|描述|
|----------------|-----------------|
|**状态**|为规则条件输入表达式。|
|**确定**|单击可以保存规则条件。|

## <a name="entering-condition-expressions"></a>输入条件表达式
 条件表达式是以文本形式输入的。 您可以键入**此。** 在编辑器中，使用类似 IntelliSense 的菜单引用工作流中使用的字段、属性和方法。 或者，可以直接键入工作流成员名称。 可以向条件中添加逻辑运算符（如 AND、OR 和 NOT）。 也可以添加谓词。 谓词由一个二元运算符和两个操作数组成。 支持的二进制运算符包括 **==** ， **>** ， **\<** ， **>=** ，并 **<=** 。 支持的操作数包括常量值、算术函数和作用域公共成员。

 您可以指定比较的类型，并且可以比较为**null**或空字符串。 您可以对包含复杂类型的变量进行嵌套的成员调用，例如，`this.Address.State == "WA"`。

 该规则条件编辑器支持以下运算符：

- 关系运算符：==、=、!=

- 比较运算符： <、\<=、>、> =

- 算术运算符：+、-、*、/、MOD

- 逻辑运算符： AND、& & 或、 &#124; &#124;、NOT、！

- 位运算符： &，&#124;

  表达式运算符优先级遵循 C# 运算符优先级规则。

  该规则条件编辑器支持以下数值表达式：

  this.i == 1D（解析为 1.0）

  this.i == 1E1（解析为 10.0）

  this.i == 1L（解析为 long 类型值）

  this.i == 1M（解析为 decimal 类型值）

  this.i == 1F（解析为 single 类型值）

  this.i == 1U（解析为 unsigned int 类型值）

  有关条件的详细信息，请参阅[在工作流中使用条件](https://msdn2.microsoft.com/library/bb628447.aspx)。

## <a name="see-also"></a>请参阅
 [IfElseActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ifelseactivity.aspx) [ConditionedActivityGroup](https://msdn2.microsoft.com/library/system.workflow.activities.conditionedactivitygroup.aspx) [ReplicatorActivity](https://msdn2.microsoft.com/library/system.workflow.activities.replicatoractivity.aspx) [WhileActivity](https://msdn2.microsoft.com/library/system.workflow.activities.whileactivity.aspx) "[选择条件" 对话框（旧版）](../workflow-designer/select-condition-dialog-box-legacy.md) [使用工作流中的条件](https://msdn2.microsoft.com/library/bb628447.aspx) [Windows Workflow Foundation UI 帮助](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)
