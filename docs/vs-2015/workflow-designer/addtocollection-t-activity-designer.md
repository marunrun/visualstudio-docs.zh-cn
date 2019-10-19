---
title: AddToCollection &lt;T &gt; 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.AddToCollection`1.UI
ms.assetid: f7fc0702-164e-4370-8946-bb2f9f9384b7
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 50deab447b3dcb93d352e73fc4765d913b4d24bf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659205"
---
# <a name="addtocollectionlttgt-activity-designer"></a>AddToCollection &lt;T &gt; 活动设计器
**AddToCollection \<T >** 活动设计器用于创建和配置 <xref:System.Activities.Statements.AddToCollection%601> 活动。

## <a name="the-addtocollectiont-activity"></a>AddToCollection \<T > 活动
 <xref:System.Activities.Statements.AddToCollection%601> 活动向集合添加一项。

### <a name="using-the-addtocollectiont-activity-designer"></a>使用 AddToCollection \<T > 活动设计器
 **AddToCollection \<T >** 活动设计器可在 "**工具箱**" 的 "**集合**" 类别中找到，该类别可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 的 "**工具箱**" 选项卡（或者 **，从**"**视图**" 菜单或 CTRL + ALT + X。）

 可以将 " **AddToCollection" \<T >** 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，例如在 <xref:System.Activities.Statements.Sequence> 中。 这将创建一个 <xref:System.Activities.Statements.AddToCollection%601> 活动，其中默认 <xref:System.Activities.Activity.DisplayName%2A> 为 AddToCollection \<Int32 >。 （默认情况下， *TypeArgument*为**Int32**。 可在属性网格中更改此项。）可以在**AddToCollection \<T >** 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。 其他属性必须在属性网格上编辑。

### <a name="the-addtocollectiont-properties"></a>AddToCollection \<T > 属性
 下表列出 <xref:System.Activities.Statements.AddToCollection%601> 属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.AddToCollection%601> 活动的友好名称。 默认值为 AddToCollection \<Int32 >。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.AddToCollection%601.Item%2A>|True|要添加到集合中的项 \<T >。 此项的类型为*T*，类型为*TypeArgument*。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.AddToCollection%601.Collection%2A>|True|项应添加到的集合。 此集合的类型为**ICollection \<TypeArgument >** 。 若要指定集合，请在属性网格中键入 Visual Basic 表达式。|
|*TypeArgument*|True|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，此*TypeArgument*类型设置为**Int32**。 若要更改类型，请在属性网格的组合框中更改 " *TypeArgument* " 的值。|

## <a name="see-also"></a>请参阅
 [集合](../workflow-designer/collection-activity-designers.md) [AddToCollection \<T > 活动设计器](../workflow-designer/addtocollection-t-activity-designer.md) [ClearCollection \<T >](../workflow-designer/clearcollection-t-activity-designer.md) [ExistsInCollection \<T](../workflow-designer/existsincollection-t-activity-designer.md) > [RemoveFromCollection \<T](../workflow-designer/removefromcollection-t-activity-designer.md) >