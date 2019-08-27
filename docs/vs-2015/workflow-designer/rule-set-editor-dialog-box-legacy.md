---
title: 规则集编辑器对话框 （旧版） |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 862842bd41762b15a38254c9d5e21bf06cdca10a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703199"
---
# <a name="rule-set-editor-dialog-box-legacy"></a>“规则集编辑器”对话框（旧版）
本主题介绍如何使用**规则集编辑器**对话框中，在旧[!INCLUDE[wfd1](../includes/wfd1-md.md)]。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。  
  
 **规则集编辑器**对话框用于创建和修改[PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)规则集，这些规则将序列化为.rules 文件。  
  
> [!NOTE]
> 如果你想要打开.rules 文件**带编码的 XML 编辑器**，必须先关闭工作流或活动的关联设计器窗口。  
  
 有关如何访问信息**规则集编辑器**对话框中，请参阅[如何：创建 PolicyActivity 规则集 （旧版）](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md)。  
  
> [!WARNING]
> 用于面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 的规则编辑器不支持多目标。  
  
 下表介绍的用户界面 (UI) 元素**规则集编辑器**对话框。  
  
|UI 元素|描述|  
|----------------|-----------------|  
|**添加规则**|向规则集中添加一个新规则定义。|  
|**删除**|从规则集中删除选定的规则。|  
|**链接**|指定要将哪种类型的正向链接用于规则集。 可用选项为：<br /><br /> -   **完全链接**，它指定要使用所有正向链接机制： 隐式的方法属性设置，并显式使用**更新**函数。<br />-   **顺序**，该值指定不使用任何正向链接。<br />-   **仅显式更新**，它指定仅执行正向链接上**更新**操作。<br /><br /> 有关正向链接的详细信息，请参阅[使用 PolicyActivity 活动](http://go.microsoft.com/fwlink?LinkID=65004)。|  
|**名称**|规则集列表的列标题。 单击可按名称对规则列表排序。|  
|**优先级**|规则集列表的列标题。 单击可按优先级对规则列表排序。|  
|**重新评估**|规则集列表的列标题。 单击可按重新计算类型对规则列表排序。|  
|**规则预览**|规则集列表的列标题。 单击可按规则的条件和操作预览对规则列表排序。|  
|**名称：**|输入规则的名称。|  
|**优先级：**|为规则输入一个优先级。 默认优先级是 0。|  
|**重新评估：**|指定要将哪种规则重新计算类型用于规则。 可用选项为：<br /><br /> -   **始终**，这将导致根据需要重新计算规则。<br />-   **永远不会**，这将导致永远不会重新计算规则。 在此情况下，规则只执行一次。|  
|**Active**|选中以激活规则。|  
|**条件：**|为规则条件输入一个表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|  
|**Then 操作：**|为 Then 操作输入表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|  
|**Else 操作：**|为 Else 操作输入表达式。 有关表达式语法的信息，请参见本页的“输入条件和操作表达式”一节。|  
|**还行**|单击可将规则集保存为 .rules 文件。|  
  
 有关规则集的详细信息，请参阅[使用 PolicyActivity 活动](http://go.microsoft.com/fwlink?LinkID=65004)。  
  
## <a name="entering-condition-and-action-expressions"></a>输入条件和操作表达式  
 输入表达式的条件以及 Then 和 Else 为其各自的文本框中的文本操作框**规则集编辑器**对话框。 您可以键入**这。** 要引用字段、 属性和方法在工作流中使用的编辑器，使用 IntelliSense 类型的菜单。 或者，可以直接键入工作流成员名称。 通过键入后跟方法名称的类名，您可以对引用的类型调用静态方法。  
  
 可以向条件中添加逻辑运算符（如 AND、OR 和 NOT）。 也可以添加谓词。 谓词由一个二元运算符和两个操作数组成。 支持的二进制运算符包括 = =、 >、 \<，> =、 和 < =。 支持的操作数包括常量值、算术函数和作用域公共成员。  
  
 您可以指定的类型进行比较，并可以与进行比较**null**或空字符串。 您可以嵌套包含复杂类型的变量成员调用，例如，`this.Address.State == "WA"`。  
  
 表达式支持下列运算符：  
  
- 关系运算符：==、=、!=  
  
- 比较运算符： <， \<=、 >、 > =  
  
- 算术运算符：+、-、*、/、MOD  
  
- 逻辑运算符：AND, &&, OR, &#124;&#124;, NOT, !  
  
- 按位运算符： &，&#124;  
  
  表达式运算符优先级遵循 C# 运算符优先级规则。  
  
  有关条件的详细信息，请参阅[在工作流中使用条件](https://msdn.microsoft.com/541211f5-d382-4810-894f-71f00b34fa77)。  
  
### <a name="halt-and-update-functions"></a>Halt 和 Update 函数  
 **Then 操作：** 并**Else 操作：** 表达式支持**暂停**并**更新**函数。 若要使用**暂停**函数中，键入**暂停**到**Then 操作：** 或**Else 操作：** 文本框。 **暂停**操作会导致规则集执行立即停止，并将控制权返回到调用代码。 您使用**更新**与正向链接的函数。  
  
 **更新**语句可以在两种形式之一在编辑器中以表示; 这两种形式显示在下面的示例：  
  
```  
Update(this.Address.State)  
Update("this/Address/State")  
```  
  
 有关使用详细信息**更新**与正向链接，请参阅[使用 PolicyActivity 活动](http://go.microsoft.com/fwlink?LinkID=65004)。  
  
## <a name="see-also"></a>请参阅  
 [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)   
 [选择规则集对话框 （旧版）](../workflow-designer/select-rule-set-dialog-box-legacy.md)   
 [使用 PolicyActivity 活动](http://go.microsoft.com/fwlink?LinkID=65004)   
 [在工作流中使用条件](http://go.microsoft.com/fwlink?LinkID=65009)