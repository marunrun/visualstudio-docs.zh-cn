---
title: ExistsInCollection&lt;T&gt;活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ExistsInCollection`1.UI
ms.assetid: 0acf9a13-caf5-4bb4-ba22-ec37d2b7267a
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 263bbf16c72bab5a42dc0ba1465d4c7062333071
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952822"
---
# <a name="existsincollectionlttgt-activity-designer"></a>ExistsInCollection&lt;T&gt;活动设计器
**ExistsInCollection\<T >** 活动设计器用于创建和配置<xref:System.Activities.Statements.ExistsInCollection%601>活动。  
  
## <a name="the-existsincollectiont-activity"></a>ExistsInCollection\<T > 活动  
 <xref:System.Activities.Statements.ExistsInCollection%601> 活动确定特定集合中是否存在指定项。  
  
### <a name="using-the-existsincollectiont-activity-designer"></a>使用 ExistsInCollection\<T > 活动设计器  
 **ExistsInCollection\<T >** 活动设计器可在**集合**类别**工具箱**，这通过单击访问**工具箱**选项卡[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **ExistsInCollection\<T >** 活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的如内部<xref:System.Activities.Statements.Sequence>。 这将创建<xref:System.Activities.Statements.ExistsInCollection%601>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>ExistsInCollection 的\<Int32 >。 (默认情况下*TypeArgument*是**Int32**。 可在属性网格中更改此值。）<xref:System.Activities.Activity.DisplayName%2A>值可以在的标头中编辑**ExistsInCollection\<T >** 活动设计器中或在**DisplayName**属性网格的框。 其他属性必须在属性网格上编辑。  
  
### <a name="the-existsincollectiont-properties"></a>ExistsInCollection\<T > 属性  
 下表列出 <xref:System.Activities.Statements.ExistsInCollection%601> 属性并说明如何在设计器中使用它们。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.ExistsInCollection%601> 活动的友好名称。 默认值为 ExistsInCollection\<Int32 >。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|  
|<xref:System.Activities.Statements.ExistsInCollection%601.Item%2A>|True|要添加到集合的项\<T >。 此项的类型是*T*属于类型*TypeArgument*。 若要指定项，请在属性网格中键入 Visual Basic 表达式。|  
|<xref:System.Activities.Statements.ExistsInCollection%601.Collection%2A>|True|项应添加到的集合。 此集合属于类型**ICollection\<TypeArgument >。** 若要指定集合，请在属性网格中键入 Visual Basic 表达式。|  
|*TypeArgument*|True|包含在 <xref:System.Collections.Generic.ICollection%601> 中的项的类型 T。 默认情况下，这*TypeArgument*类型设置为**Int32**。 若要更改的类型，更改的值*TypeArgument*在属性网格中的组合框中。|  
|<xref:System.Activities.Activity%601.Result%2A>|False|一个指示集合中是否存在指定项的值。 若要指定要绑定到结果的变量，请在属性网格中键入 Visual Basic 变量。|  
  
## <a name="see-also"></a>请参阅  
 [集合](../workflow-designer/collection-activity-designers.md)   
 [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)   
 [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)   
 [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)