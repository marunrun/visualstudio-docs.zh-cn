---
title: 工作流设计器-交换机<T>活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.ModelItemKeyValuePair.UI
- System.Activities.Statements.Switch`1.UI
ms.assetid: 18a6c96e-49a9-4356-ab61-fbd7e3ab44bb
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7eb83567a7d59dc02779839a5305b9c1c0329912
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62434041"
---
# <a name="switcht-activity-designer"></a>交换机\<T > 活动设计器

<xref:System.Activities.Statements.Switch%601> 活动计算指定表达式并执行活动集合中其关联键与计算所得值匹配的活动。

**交换机 < T\>** 活动设计器用于创建和配置<xref:System.Activities.Statements.Switch%601>工作流设计器中的活动。

## <a name="the-switchtactivity"></a>开关\<T > 活动

一个 <xref:System.Activities.Statements.Switch%601> 活动包含一个 <xref:System.Activities.Statements.Switch%601.Expression%2A> 和一个 <xref:System.Activities.Statements.Switch%601.Cases%2A> 的字典。 字典中的每个示例包含一个对，包含*键*并用作其对应的活动*值*。 <xref:System.Activities.Statements.Switch%601> 活动计算 <xref:System.Activities.Statements.Switch%601.Expression%2A> 并将其与每个键相比较。 如果找到匹配项，则会执行对应的活动。 只可能有一个匹配项，因为字典键与字典的相等比较器所定义的相等类型的对应必须是唯一的。 如果未找到匹配项，则会执行 <xref:System.Activities.Statements.Switch%601.Default%2A> 活动。

## <a name="how-to-use-the-switcht-activity-designer"></a>如何使用开关\<T > 活动设计器

访问**交换机\<T >** 活动设计器中的**控制流**类别**工具箱**。 将它放到工作流设计器之后, 它将显示**选择类型**对话框，以允许用户指定的泛型类型*T*中使用<xref:System.Activities.Statements.Switch%601>活动。 默认值是**Int32**。 一次的泛型类型*T*已选择**交换机 < T\>** 设计器添加到工作流设计器。

以下是的属性**交换机 < T\>** 设计器。 所有这些属性都可以在属性网格中进行编辑。 其中一些属性还可以在设计器图面上进行编辑。

下表列出最有用的 <xref:System.Activities.Statements.Switch%601> 属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Switch%601> 活动设计器的友好名称。 默认值为 Switch < Int32\>。 可以在编辑该值**属性**窗口或直接在设计器的标头。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.Switch%601.Expression%2A>|True|指定用于与 case 集合中的键进行比较以确定执行哪个 case 的表达式。|
|<xref:System.Activities.Statements.Switch%601.Default%2A>||指定未找到匹配项时执行的活动。 单击**添加活动**以打开设计器上的按钮**默认**框可放置在活动的位置。|
|<xref:System.Activities.Statements.Switch%601.Cases%2A>||指定要计算的 case。 若要添加 case，请单击**添加新的用例**底部的按钮**交换机\<T >** 设计器。 该按钮将变为文本框 (如果添加此开关时选择的泛型类型的组合框\<T > 为 String 或 Enum)。 添加中的键后**Case 值**框中，case 区域将展开，可以删除活动的提示文本"此处放置活动"来定义这种情况的执行逻辑。|

可以添加多个 case，但 case 键不能重复。 否则将显示一个错误对话框，报告指定 case 键已存在，您必须选择其他键。 在中**交换机\<T >** 设计器中，只有一个 case 区域能以一次展开的视图。 某个 case 区域为折叠的视图时，单击该 case 区域即可展开它。 请注意，对于折叠的 case，如果该活动有显示名称，设计器将在该 case 内的右侧显示该显示名称。 否则，它会显示**添加活动**按钮，展开 case，如果您单击它，并允许您添加的活动。

单击现有 case 的键可将该键从标签变为文本框，从而可以编辑该 case 键。

删除 case 的方法有两种：

- 选中相应 case，然后删除它。

- 选择 case，右击以显示上下文菜单并选择**删除**。

请注意，必须选中 case 本身才能删除它。 选中并删除 case 内的活动只会删除该活动而不会删除该 case。

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)