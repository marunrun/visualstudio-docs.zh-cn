---
title: 工作流设计器-Switch <T> 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.ModelItemKeyValuePair.UI
- System.Activities.Statements.Switch`1.UI
ms.assetid: 18a6c96e-49a9-4356-ab61-fbd7e3ab44bb
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1afda542dd3f45e5be723ce35b2546626f3679e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72649900"
---
# <a name="switcht-activity-designer"></a>切换 \<T > 活动设计器

<xref:System.Activities.Statements.Switch%601> 活动计算指定表达式并执行活动集合中其关联键与计算所得值匹配的活动。

**开关 < T \>** 活动设计器用于在工作流设计器中创建和配置 <xref:System.Activities.Statements.Switch%601> 活动。

## <a name="the-switchtactivity"></a>切换 \<T > 活动

一个 <xref:System.Activities.Statements.Switch%601> 活动包含一个 <xref:System.Activities.Statements.Switch%601.Expression%2A> 和一个 <xref:System.Activities.Statements.Switch%601.Cases%2A> 的字典。 字典中的每个用例都由一个对，其中包含一个*键*和一个充当其对应*值*的活动。 <xref:System.Activities.Statements.Switch%601> 活动计算 <xref:System.Activities.Statements.Switch%601.Expression%2A> 并将其与每个键相比较。 如果找到匹配项，则会执行对应的活动。 只可能有一个匹配项，因为字典键与字典的相等比较器所定义的相等类型的对应必须是唯一的。 如果未找到匹配项，则会执行 <xref:System.Activities.Statements.Switch%601.Default%2A> 活动。

## <a name="how-to-use-the-switcht-activity-designer"></a>如何使用开关 \<T > 活动设计器

在 "**工具箱**" 的 "**控制流**" 类别中访问**开关 \<T >** 活动设计器。 将其放入工作流设计器后，它将显示 "**选择类型**" 对话框，让用户指定 <xref:System.Activities.Statements.Switch%601> 活动中使用的泛型类型*T* 。 默认值为**Int32**。 选择泛型类型*t*后， **< T \>** 设计器的开关将添加到工作流设计器中。

下面是**Switch < T \>** 设计器的属性。 所有这些属性都可以在属性网格中进行编辑。 其中一些属性还可以在设计器图面上进行编辑。

下表列出最有用的 <xref:System.Activities.Statements.Switch%601> 属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Switch%601> 活动设计器的友好名称。 默认值为 Switch < Int32 \>。 该值可以在 "**属性**" 窗口中编辑，也可以直接在设计器标头中编辑。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.Switch%601.Expression%2A>|True|指定用于与 case 集合中的键进行比较以确定执行哪个 case 的表达式。|
|<xref:System.Activities.Statements.Switch%601.Default%2A>||指定未找到匹配项时执行的活动。 单击设计器上的 "**添加活动**" 按钮，以打开可以删除活动的**默认**框。|
|<xref:System.Activities.Statements.Switch%601.Cases%2A>||指定要计算的 case。 若要添加事例，请单击**Switch \<T >** 设计器底部的 "**添加新事例**" 按钮。 如果在添加开关时选择的泛型类型 \<T > 为字符串或枚举，则该按钮将更改为文本框（组合框）。 在 " **case 值**" 框中添加了一个键后，将展开事例区域，并且可以在提示文本 "在此处放置活动" 时删除一个活动以定义该事例的执行逻辑。|

可以添加多个 case，但 case 键不能重复。 否则将显示一个错误对话框，报告指定 case 键已存在，您必须选择其他键。 在**Switch \<T >** 设计器中，一次只能有一个 case 区域处于展开视图中。 某个 case 区域为折叠的视图时，单击该 case 区域即可展开它。 请注意，对于折叠的 case，如果该活动有显示名称，设计器将在该 case 内的右侧显示该显示名称。 否则，它会显示 "**添加活动**" 按钮，该按钮可在您单击案例并允许您添加活动时展开案例。

单击现有 case 的键可将该键从标签变为文本框，从而可以编辑该 case 键。

删除 case 的方法有两种：

- 选中相应 case，然后删除它。

- 选择事例，右键单击以显示上下文菜单，然后选择 "**删除**"。

请注意，必须选中 case 本身才能删除它。 选中并删除 case 内的活动只会删除该活动而不会删除该 case。

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)