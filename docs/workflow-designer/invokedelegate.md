---
title: 工作流设计器-InvokeDelegate
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
author: jillre
ms.openlocfilehash: 5227d96e3fad03dd3e3309523a6d2c68a1abdc11
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650183"
---
# <a name="invokedelegate"></a>InvokeDelegate

**InvokeDelegate**设计器用于创建和配置 <xref:System.Activities.Statements.InvokeDelegate> 活动。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate 活动

<xref:System.Activities.Statements.InvokeDelegate> 调用公共委托。

### <a name="use-the-invokedelegate-activity-designer"></a>使用 InvokeDelegate 活动设计器

访问 "**工具箱**" 的 "**基元**" 类别中的 " **InvokeDelegate** " 活动设计器。 可以将 " **InvokeDelegate** " 活动设计器从 "**工具箱**" 拖放到工作流设计器表面上，通常会在其中放置活动，如 <xref:System.Activities.Statements.Sequence> 内。 删除活动设计器将创建一个 <xref:System.Activities.Statements.InvokeDelegate> 的活动，其默认 <xref:System.Activities.Activity.DisplayName%2A> 为 InvokeDelegate。 可以在 " **InvokeDelegate** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate 属性

下表列出 <xref:System.Activities.Statements.InvokeDelegate> 属性并说明如何在设计器中使用它们。 这些属性可在属性网格中进行编辑，某些属性可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.InvokeDelegate> 活动的友好名称。 默认值为 InvokeDelegate。<br /><br /> 尽管不是严格需要 <xref:System.Activities.Activity.DisplayName%2A>，但最好是使用一个。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|True|要在执行活动时调用的 <xref:System.Activities.ActivityDelegate> 的名称。 此属性可以在设计器图面上进行编辑，并且是必需的。|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|False|调用委托的参数集合。 密钥是 <xref:System.Activities.ActivityDelegate> 上参数对象的名称，值是计算表达式并将其分配给相应参数对象的参数。 若要显示可在其中设置此属性的 " **DelegateArguments** " 对话框，请单击 "属性" 网格的 " **DelegateArguments** " 字段中的省略号按钮。 单击 "**创建自变量**" 字段以添加参数。|

## <a name="see-also"></a>请参阅

- [如何：在工作流设计器中定义和使用活动委托](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)