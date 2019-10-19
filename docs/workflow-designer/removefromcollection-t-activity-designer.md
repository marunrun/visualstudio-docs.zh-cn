---
title: RemoveFromCollection &lt;T &gt; 活动设计器工作流设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.RemoveFromCollection`1.UI
ms.assetid: 6617ba26-c8bc-4aed-b746-112bf490d288
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1a8885505607d654327ad9dc36ab88708ab708c3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650018"
---
# <a name="removefromcollectiont-activity-designer"></a>RemoveFromCollection \<T > 活动设计器

**RemoveFromCollection \<T >** 活动设计器用于创建和配置 <xref:System.Activities.Statements.RemoveFromCollection%601> 活动。

## <a name="the-removefromcollectiontactivity"></a>RemoveFromCollection \<T > 活动

<xref:System.Activities.Statements.RemoveFromCollection%601> 活动从特定集合中移除指定项。

### <a name="using-the-removefromcollectiont-activity-designer"></a>使用 RemoveFromCollection \<T > 活动设计器

访问 "**工具箱**" 的 "**集合**" 类别中的 " **RemoveFromCollection \<T >** " 活动设计器。
可以将 " **RemoveFromCollection" \<T >** 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置，例如在 <xref:System.Activities.Statements.Sequence> 中。 这将创建一个 <xref:System.Activities.Statements.RemoveFromCollection%601> 活动，其中默认 <xref:System.Activities.Activity.DisplayName%2A> 为 RemoveFromCollection < Int32 \>。 可以在**RemoveFromCollection < t \>** 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。 其他属性必须在属性网格上编辑。

### <a name="the-removefromcollectiont-properties"></a>RemoveFromCollection < T \> 属性

下表显示 <xref:System.Activities.Statements.RemoveFromCollection%601> 属性，并说明如何在设计器中使用它们：

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.RemoveFromCollection%601> 活动的可选友好名称。 默认值为 RemoveFromCollection < Int32 \>。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Item%2A>|True|要从集合中移除的项 **\<T >** 。 此项的类型为*T*，类型为*TypeArgument*。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Collection%2A>|True|应从中移除项的集合。 此集合的类型为**ICollection < TypeArgument \>。** 若要指定集合，请在属性网格中键入 Visual Basic 表达式。|
|*TypeArgument*|True|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，此*TypeArgument*类型设置为**Int32**。 若要更改类型，请在属性网格的组合框中更改 " *TypeArgument* " 的值。|
|<xref:System.Activities.Activity%601.Result%2A>|False|一个指示指定项是否已从集合中移除的值。 若要指定要绑定到结果的变量，请在属性网格中键入一个变量。|

## <a name="see-also"></a>请参阅

- [收集](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)