---
title: 工作流设计器-RemoveFromCollection&lt;T&gt;活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.RemoveFromCollection`1.UI
ms.assetid: 6617ba26-c8bc-4aed-b746-112bf490d288
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4b3a43c05f8be4806cf10098a4df673903494756
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62933739"
---
# <a name="removefromcollectiont-activity-designer"></a>RemoveFromCollection\<T > 活动设计器

**RemoveFromCollection\<T >** 活动设计器用于创建和配置<xref:System.Activities.Statements.RemoveFromCollection%601>活动。

## <a name="the-removefromcollectiontactivity"></a>RemoveFromCollection\<T > 活动

<xref:System.Activities.Statements.RemoveFromCollection%601> 活动从特定集合中移除指定项。

### <a name="using-the-removefromcollectiont-activity-designer"></a>使用 RemoveFromCollection\<T > 活动设计器

访问**RemoveFromCollection\<T >** 活动设计器中的**集合**类别**工具箱**。
**RemoveFromCollection\<T >** 活动设计器可以从拖动**工具箱**和无论通常放置活动的如在何处放置到工作流设计器图面内部<xref:System.Activities.Statements.Sequence>。 这将创建<xref:System.Activities.Statements.RemoveFromCollection%601>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>RemoveFromCollection 的 < Int32\>。 <xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**RemoveFromCollection < T\>** 活动设计器中或在**DisplayName**属性网格的框。 其他属性必须在属性网格上编辑。

### <a name="the-removefromcollectiont-properties"></a>RemoveFromCollection < T\>属性

下表显示<xref:System.Activities.Statements.RemoveFromCollection%601>属性并说明如何在设计器中使用：

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.RemoveFromCollection%601> 活动的可选友好名称。 默认值为 RemoveFromCollection < Int32\>。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Item%2A>|True|要移除的项**集合\<T >**。 此项的类型是*T*，它属于类型*TypeArgument*。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Collection%2A>|True|应从中删除项的集合。 此集合属于类型**ICollection < TypeArgument\>。** 若要指定集合，请键入在属性网格中的 Visual Basic 表达式。|
|*TypeArgument*|True|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，这*TypeArgument*类型设置为**Int32**。 若要更改的类型，更改的值*TypeArgument*在属性网格中的组合框中。|
|<xref:System.Activities.Activity%601.Result%2A>|False|一个指示指定项是否已从集合中移除的值。 若要指定要绑定到结果的变量，请在属性网格中键入一个变量。|

## <a name="see-also"></a>请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)