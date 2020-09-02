---
title: ExistsInCollection &lt; T &gt; 活动设计器工作流设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ExistsInCollection`1.UI
ms.assetid: 0acf9a13-caf5-4bb4-ba22-ec37d2b7267a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b48bb11e2aac9d542a07551df62d710c41596d28
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86875652"
---
# <a name="existsincollectiont-activity-designer"></a>ExistsInCollection\<T> 活动设计器

" **ExistsInCollection \<T> ** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.ExistsInCollection%601> 活动。

## <a name="the-existsincollectiont-activity"></a>ExistsInCollection \<T> 活动

<xref:System.Activities.Statements.ExistsInCollection%601> 活动确定特定集合中是否存在指定项。

### <a name="using-the-existsincollectiont-activity-designer"></a>使用 ExistsInCollection \<T> 活动设计器

" **ExistsInCollection \<T> ** " 活动设计器可在 "**工具箱**" 的 "**集合**" 类别中找到，可通过单击工作流设计器的 "**工具箱**" 选项卡进行访问。 或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** + **Alt** + **X**。

可以将 " ** \<T> ExistsInCollection** " 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 这将创建一个 <xref:System.Activities.Statements.ExistsInCollection%601> 活动，其默认值为 <xref:System.Activities.Activity.DisplayName%2A> ExistsInCollection<Int32 \> 。  (默认情况下， *TypeArgument* 为 **Int32**。 可以在属性网格中更改此值。 ) <xref:System.Activities.Activity.DisplayName%2A> 可以在**ExistsInCollection<T \> **活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑值。 其他属性必须在属性网格上编辑。

### <a name="the-existsincollectiont-properties"></a>ExistsInCollection \<T> 属性

下表显示了 <xref:System.Activities.Statements.ExistsInCollection%601> 这些属性，并说明了如何在设计器中使用这些属性：

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.ExistsInCollection%601> 活动的友好名称。 默认值为 ExistsInCollection<Int32 \> 。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Item%2A>|正确|要在集合中查找的项 \<T> 。 此项的类型为 *T*，类型为 *TypeArgument*。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Collection%2A>|正确|要在其中检查项是否存在的集合。 此集合的类型为 **ICollection<TypeArgument \> 。** 若要指定集合，请在属性网格中键入 Visual Basic 表达式。|
|*TypeArgument*|正确|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，此 *TypeArgument* 类型设置为 **Int32**。 若要更改类型，请在属性网格的组合框中更改 " *TypeArgument* " 的值。|
|<xref:System.Activities.Activity%601.Result%2A>|错误|一个指示集合中是否存在指定项的值。 若要指定要绑定到结果的变量，请在属性网格中键入 Visual Basic 变量。|

## <a name="see-also"></a>另请参阅

- [集合](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)