---
title: 工作流设计器-InvokeDelegate
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 511d73ea2992887f31bc8750cc9ba32934bddd91
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62537083"
---
# <a name="invokedelegate"></a>InvokeDelegate

**InvokeDelegate**设计器用于创建和配置<xref:System.Activities.Statements.InvokeDelegate>活动。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate 活动

<xref:System.Activities.Statements.InvokeDelegate> 调用公共委托。

### <a name="use-the-invokedelegate-activity-designer"></a>使用 InvokeDelegate 活动设计器

访问**InvokeDelegate**中的活动设计器**基元**类别**工具箱**。 **InvokeDelegate**活动设计器可以从拖动**工具箱**并在任何位置通常放置活动的例如内放置到工作流设计器图面<xref:System.Activities.Statements.Sequence>。 放置在活动设计器创建<xref:System.Activities.Statements.InvokeDelegate>默认值的活动<xref:System.Activities.Activity.DisplayName%2A>InvokeDelegate。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**InvokeDelegate**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate 属性

下表列出 <xref:System.Activities.Statements.InvokeDelegate> 属性并说明如何在设计器中使用它们。 可以在属性网格中编辑这些属性，一些可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.InvokeDelegate> 活动的友好名称。 默认值为 InvokeDelegate。<br /><br /> 尽管<xref:System.Activities.Activity.DisplayName%2A>并不严格要求，最好是使用其中一个。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|True|要在执行活动时调用的 <xref:System.Activities.ActivityDelegate> 的名称。 此属性可编辑设计器图面，并且是必需的。|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|False|调用委托的参数集合。 键是参数对象的名称上<xref:System.Activities.ActivityDelegate>，而值是其表达式进行计算并分配到相应的参数对象的参数。 若要显示**DelegateArguments**对话框中，你可以设置此属性，请单击中的省略号按钮**DelegateArguments**属性网格的字段。 单击**创建自变量**字段以添加自变量。|

## <a name="see-also"></a>请参阅

- [如何：在工作流设计器中定义和使用活动委托](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)