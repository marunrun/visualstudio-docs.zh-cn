---
title: Rule Set Editor Dialog Box (Legacy) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Rules.Design.RuleSetDialog.UI
helpviewer_keywords:
- Rule Set Editor dialog box
ms.assetid: 7cfd5df1-1115-4e5c-9b72-121f39419e83
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 83cdd4f549655be524abdd2a4708b316f6747b3e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302764"
---
# <a name="rule-set-editor-dialog-box-legacy"></a>“规则集编辑器”对话框（旧版）
This topic describes how use the **Rule Set Editor** dialog box in the legacy [!INCLUDE[wfd1](../includes/wfd1-md.md)]. 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 The **Rule Set Editor** dialog box is used to create and modify [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) rule sets, which are serialized to a .rules file.

> [!NOTE]
> If you want to open the .rules file with the **XML Editor with encoding**, you must first close the associated designer window for the workflow or activity.

 For information about how to access the **Rule Set Editor** dialog box, see [How to: Create a PolicyActivity Rule Set (Legacy)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md).

> [!WARNING]
> 用于面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 的规则编辑器不支持多目标。

 The following table describes the user interface (UI) elements of the **Rule Set Editor** dialog box.

|UI 元素|描述|
|----------------|-----------------|
|**Add Rule**|向规则集中添加一个新规则定义。|
|**删除**|从规则集中删除选定的规则。|
|**Chaining**|指定要将哪种类型的正向链接用于规则集。 可用选项为：<br /><br /> -   **Full Chaining**, which specifies to use all forward chaining mechanisms: implicit, method attributing, and explicit using an **Update** function.<br />-   **Sequential**, which specifies not to use any forward chaining.<br />-   **Explicit Update Only**, which specifies to only perform forward chaining on **Update** actions.<br /><br /> For more information about forward chaining, see [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004).|
|**名称**|规则集列表的列标题。 单击可按名称对规则列表排序。|
|**Priority**|规则集列表的列标题。 单击可按优先级对规则列表排序。|
|**Reevaluation**|规则集列表的列标题。 单击可按重新计算类型对规则列表排序。|
|**Rule Preview**|规则集列表的列标题。 单击可按规则的条件和操作预览对规则列表排序。|
|**Name：**|输入规则的名称。|
|**Priority:**|为规则输入一个优先级。 默认优先级是 0。|
|**Reevaluation:**|指定要将哪种规则重新计算类型用于规则。 可用选项为：<br /><br /> -   **Always**, which causes the rule to be reevaluated as needed.<br />-   **Never**, which causes the rule to never be reevaluated. 在此情况下，规则只执行一次。|
|**Active**|选中以激活规则。|
|**Condition:**|为规则条件输入一个表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|
|**Then Actions:**|为 Then 操作输入表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|
|**Else Actions:**|为 Else 操作输入表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|
|**OK**|单击可将规则集保存为 .rules 文件。|

 For more information about rule sets, see [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004).

## <a name="entering-condition-and-action-expressions"></a>输入条件和操作表达式
 You enter expressions for the Condition and the Then and Else actions as text in their respective text boxes in the **Rule Set Editor** dialog box. You can type **this.** into the editor to reference fields, properties and methods used in the workflow, using an IntelliSense-type of menu. 或者，可以直接键入工作流成员名称。 通过键入后跟方法名称的类名，您可以对引用的类型调用静态方法。

 可以向条件中添加逻辑运算符（如 AND、OR 和 NOT）。 也可以添加谓词。 谓词由一个二元运算符和两个操作数组成。 The binary operators supported are ==, >, \<, >=, and <=. 支持的操作数包括常量值、算术函数和作用域公共成员。

 You can specify the type for the comparison, and you can compare to **null** or an empty string. 您可以嵌套包含复杂类型的变量成员调用，例如，`this.Address.State == "WA"`。

 表达式支持下列运算符：

- 关系运算符：==、=、!=

- Comparison operators: <, \<=, >, >=

- 算术运算符：+、-、*、/、MOD

- Logical operators: AND, &&, OR, &#124;&#124;, NOT, !

- Bitwise operators: &, &#124;

  表达式运算符优先级遵循 C# 运算符优先级规则。

  For more information about conditions, see [Using Conditions in Workflows](https://msdn.microsoft.com/541211f5-d382-4810-894f-71f00b34fa77).

### <a name="halt-and-update-functions"></a>Halt 和 Update 函数
 **Then Actions:** and **Else Actions:** expressions support **Halt** and **Update** functions. To use the **Halt** function, type **Halt** into a **Then Action:** or **Else Action:** text box. The **Halt** action causes rule set execution to stop immediately, and control returns to the calling code. You use the **Update** function with forward chaining.

 An **Update** statement can be expressed in the editor in one of two forms; both forms are shown in the following example:

```
Update(this.Address.State)
Update("this/Address/State")
```

 For more information about using **Update** with forward chaining, see [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004).

## <a name="see-also"></a>请参阅
 [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) [Select Rule Set Dialog Box (Legacy)](../workflow-designer/select-rule-set-dialog-box-legacy.md) [Using the PolicyActivity Activity](https://go.microsoft.com/fwlink?LinkID=65004) [Using Conditions in Workflows](https://go.microsoft.com/fwlink?LinkID=65009)