---
title: "\"规则集编辑器\" 对话框（旧版） |Microsoft Docs"
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
ms.openlocfilehash: 8010bbbc38dee980ebe89dc60ccb513379103a26
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846318"
---
# <a name="rule-set-editor-dialog-box-legacy"></a>“规则集编辑器”对话框（旧版）
本主题介绍如何使用旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)]中的 "**规则集编辑器**" 对话框。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 "**规则集编辑器**" 对话框用于创建和修改序列化为 rules 文件的[PolicyActivity](https://msdn2.microsoft.com/library/system.workflow.activities.policyactivity.aspx)规则集。

> [!NOTE]
> 如果要通过**包含编码的 XML 编辑器**打开 rules 文件，则必须先关闭工作流或活动的关联设计器窗口。

 有关如何访问 "**规则集编辑器**" 对话框的信息，请参阅[如何：创建 PolicyActivity 规则集（旧版）](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md)。

> [!WARNING]
> 用于面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 的规则编辑器不支持多目标。

 下表描述了 "**规则集编辑器**" 对话框的用户界面（UI）元素。

|UI 元素|描述|
|----------------|-----------------|
|**添加规则**|向规则集中添加一个新规则定义。|
|**删除**|从规则集中删除选定的规则。|
|**链接**|指定要将哪种类型的正向链接用于规则集。 可用选项为：<br /><br /> -   **完全链接**，它指定使用所有前向链接机制：隐式、方法的特性化和使用**Update**函数的显式。<br />-   **顺序**，指定不使用任何前向链接。<br />**仅 -   显式更新**，指定仅对**更新**操作执行正向链接。<br /><br /> 有关正向链接的详细信息，请参阅[使用 PolicyActivity 活动](https://msdn2.microsoft.com/library/bb675229.aspx)。|
|**Name**|规则集列表的列标题。 单击可按名称对规则列表排序。|
|**优先级**|规则集列表的列标题。 单击可按优先级对规则列表排序。|
|**评估**|规则集列表的列标题。 单击可按重新计算类型对规则列表排序。|
|**规则预览**|规则集列表的列标题。 单击可按规则的条件和操作预览对规则列表排序。|
|**Name：**|输入规则的名称。|
|**优先级：**|为规则输入一个优先级。 默认优先级是 0。|
|**评估**|指定要将哪种规则重新计算类型用于规则。 可用选项为：<br /><br /> -   **Always**，这将导致规则根据需要进行重新计算。<br />-   **从不**，这将导致规则永远不会重新计算。 在此情况下，规则只执行一次。|
|**Active**|选中以激活规则。|
|**状态**|为规则条件输入一个表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|
|**Then 操作：**|为 Then 操作输入表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|
|**Else 操作：**|为 Else 操作输入表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|
|**确定**|单击可将规则集保存为 .rules 文件。|

 有关规则集的详细信息，请参阅[使用 PolicyActivity 活动](https://msdn2.microsoft.com/library/bb675229.aspx)。

## <a name="entering-condition-and-action-expressions"></a>输入条件和操作表达式
 您可以在 "**规则集编辑器**" 对话框中的相应文本框中输入条件的表达式以及 Then 和 Else 操作的表达式。 您可以键入**此。** 在编辑器中，使用 IntelliSense 类型的菜单引用工作流中使用的字段、属性和方法。 或者，可以直接键入工作流成员名称。 通过键入后跟方法名称的类名，您可以对引用的类型调用静态方法。

 可以向条件中添加逻辑运算符（如 AND、OR 和 NOT）。 也可以添加谓词。 谓词由一个二元运算符和两个操作数组成。 支持的二进制运算符包括 = =、>、\<、> = 和 < =。 支持的操作数包括常量值、算术函数和作用域公共成员。

 您可以指定比较的类型，并且可以比较为**null**或空字符串。 您可以嵌套包含复杂类型的变量成员调用，例如，`this.Address.State == "WA"`。

 表达式支持下列运算符：

- 关系运算符：==、=、!=

- 比较运算符： <、\<=、>、> =

- 算术运算符：+、-、*、/、MOD

- 逻辑运算符： AND、& & 或、 &#124; &#124;、NOT、！

- 位运算符： &，&#124;

  表达式运算符优先级遵循 C# 运算符优先级规则。

  有关条件的详细信息，请参阅[在工作流中使用条件](https://msdn.microsoft.com/541211f5-d382-4810-894f-71f00b34fa77)。

### <a name="halt-and-update-functions"></a>Halt 和 Update 函数
 **Then 操作：** 和**Else 操作：** 表达式支持**暂停**和**更新**函数。 若要使用**暂停**功能，请键入 "**暂停**到**Then 操作：** " 或 "**操作：** " 文本框中。 **暂停**操作会立即停止规则集的执行，并将控制权返回给调用代码。 将**更新**函数用于正向链接。

 可以用以下两种形式之一在编辑器中表示**Update**语句;下面的示例演示了这两种形式：

```
Update(this.Address.State)
Update("this/Address/State")
```

 有关将**更新**与正向链接一起使用的详细信息，请参阅[使用 PolicyActivity 活动](https://msdn2.microsoft.com/library/bb675229.aspx)。

## <a name="see-also"></a>请参阅
 [PolicyActivity](https://msdn2.microsoft.com/library/system.workflow.activities.policyactivity.aspx) "[选择规则集" 对话框（旧版）](../workflow-designer/select-rule-set-dialog-box-legacy.md)使用[工作流中的条件](https://msdn2.microsoft.com/library/bb628447.aspx)[的 PolicyActivity 活动](https://msdn2.microsoft.com/library/bb675229.aspx)
