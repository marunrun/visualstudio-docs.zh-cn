---
title: 工作流设计器-ClearCollection <T> 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ClearCollection`1.UI
ms.assetid: db0e5da2-7b5a-4f1a-864c-f3aeeeeb51a7
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a4808c046c4da23bc5c95d3978965afd938962f5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650686"
---
# <a name="clearcollectiont-activity-designer"></a>ClearCollection \<T > 活动设计器

**ClearCollection \<T >** 活动设计器用于创建和配置 <xref:System.Activities.Statements.ClearCollection%601> 活动。

## <a name="the-clearcollectiont-activity"></a>ClearCollection \<T > 活动

<xref:System.Activities.Statements.ClearCollection%601> 活动可清除指定集合中的所有项。

### <a name="using-the-clearcollectiont-activity-designer"></a>使用 ClearCollection \<T > 活动设计器

**ClearCollection \<T >** 活动设计器可在 "**工具箱**" 的 "**集合**" 类别中找到，可通过单击工作流设计器的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** +**Alt** +**X**。

可以将 " **ClearCollection" \<T >** 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上放置活动的任何位置，例如在 <xref:System.Activities.Statements.Sequence> 中。 删除活动设计器将创建一个 <xref:System.Activities.Statements.ClearCollection%601> 的活动，其中默认 <xref:System.Activities.Activity.DisplayName%2A> 为 ClearCollection < Int32 \>。 （默认情况下， *TypeArgument*为**Int32**。 可以在属性网格中更改 TypeArgument。）可以在**ClearCollection < t \>** 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。 其他属性必须在属性网格上编辑。

### <a name="the-clearcollectiont-properties"></a>ClearCollection \<T > 属性

下表列出 <xref:System.Activities.Statements.ClearCollection%601> 属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.ClearCollection%601> 活动的可选友好名称。 默认值为 ClearCollection < Int32 \>。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.ClearCollection%601.Collection%2A>|True|指定要清除其中项的集合。 此集合的类型为**ICollection \<TypeArgument >。** 若要指定集合，请在属性网格中键入 Visual Basic 表达式。|
|*TypeArgument*|True|指定包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，此*TypeArgument*类型设置为**Int32**。 若要更改类型，请在属性网格的组合框中更改 " *TypeArgument* " 的值。|

## <a name="see-also"></a>请参阅

- [收集](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)