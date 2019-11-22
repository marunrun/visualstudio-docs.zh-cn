---
title: Rule Condition Editor Dialog Box (Legacy) | Microsoft Docs
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
ms.openlocfilehash: a632b90e89e58c26ec72083fe3f4ed9223826dae
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302855"
---
# <a name="rule-condition-editor-dialog-box-legacy"></a>“规则条件编辑器”对话框（旧版）
This topic describes how use the **Rule Condition Editor** dialog box in the legacy [!INCLUDE[wfd1](../includes/wfd1-md.md)]. 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 You create and modify declarative rule conditions by using the **Rule Condition Editor** dialog box. 这些规则条件作为以下 Windows Workflow Foundation 现成可用的活动属性被公开：

- [ConditionedActivityGroup](https://go.microsoft.com/fwlink?LinkID=65017)

- [IfElseBranchActivity](https://go.microsoft.com/fwlink?LinkID=65034)

- [ReplicatorActivity](https://go.microsoft.com/fwlink?LinkID=65039)

- [WhileActivity](https://go.microsoft.com/fwlink?LinkID=65049)

- [SequentialWorkflowActivity](https://go.microsoft.com/fwlink?LinkID=65040)

- [StateMachineWorkflowActivity](https://go.microsoft.com/fwlink?LinkID=65045)

  You access the **Rule Condition Editor** dialog box by using the [Select Condition Dialog Box (Legacy)](../workflow-designer/select-condition-dialog-box-legacy.md).

  The following table describes the user interface (UI) elements of the **Rule Condition Editor** dialog box.

|UI 元素|描述|
|----------------|-----------------|
|**Condition:**|为规则条件输入表达式。|
|**OK**|单击可以保存规则条件。|

## <a name="entering-condition-expressions"></a>输入条件表达式
 条件表达式是以文本形式输入的。 You can type **this.** into the editor to reference fields, properties, and methods used in the workflow, using an IntelliSense-like menu. 或者，可以直接键入工作流成员名称。 可以向条件中添加逻辑运算符（如 AND、OR 和 NOT）。 也可以添加谓词。 谓词由一个二元运算符和两个操作数组成。 The binary operators supported are **==** , **>** , **\<** , **>=** , and **<=** . 支持的操作数包括常量值、算术函数和作用域公共成员。

 You can specify the type for the comparison, and you can compare to **null** or an empty string. 您可以对包含复杂类型的变量进行嵌套的成员调用，例如，`this.Address.State == "WA"`。

 该规则条件编辑器支持以下运算符：

- 关系运算符：==、=、!=

- Comparison operators: <, \<=, >, >=

- 算术运算符：+、-、*、/、MOD

- Logical operators: AND, &&, OR, &#124;&#124;, NOT, !

- Bitwise operators: &, &#124;

  表达式运算符优先级遵循 C# 运算符优先级规则。

  该规则条件编辑器支持以下数值表达式：

  this.i == 1D（解析为 1.0）

  this.i == 1E1（解析为 10.0）

  this.i == 1L（解析为 long 类型值）

  this.i == 1M（解析为 decimal 类型值）

  this.i == 1F（解析为 single 类型值）

  this.i == 1U（解析为 unsigned int 类型值）

  For more information about conditions, see [Using Conditions in Workflows](https://go.microsoft.com/fwlink?LinkID=65009).

## <a name="see-also"></a>请参阅
 [IfElseActivity](https://go.microsoft.com/fwlink?LinkID=65033) [ConditionedActivityGroup](https://go.microsoft.com/fwlink?LinkID=65017) [ReplicatorActivity](https://go.microsoft.com/fwlink?LinkID=65039) [WhileActivity](https://go.microsoft.com/fwlink?LinkID=65049) [Select Condition Dialog Box (Legacy)](../workflow-designer/select-condition-dialog-box-legacy.md) [Using Conditions in Workflows](https://go.microsoft.com/fwlink?LinkID=65009) [Legacy Designer for Windows Workflow Foundation UI Help](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)