---
title: 工作流设计器-InvokeDelegate
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
author: TerryGLee
ms.author: tglee
ms.workload:
- multiple
ms.openlocfilehash: 9e63fb7a766b79467749cc5181a575e0d35a07b8
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86876068"
---
# <a name="invokedelegate"></a>InvokeDelegate

**InvokeDelegate**设计器用于创建和配置 <xref:System.Activities.Statements.InvokeDelegate> 活动。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate 活动

<xref:System.Activities.Statements.InvokeDelegate> 调用公共委托。

### <a name="use-the-invokedelegate-activity-designer"></a>使用 InvokeDelegate 活动设计器

访问 "**工具箱**" 的 "**基元**" 类别中的 " **InvokeDelegate** " 活动设计器。 可以将 " **InvokeDelegate** " 活动设计器从 "**工具箱**" 拖放到工作流设计器表面上，通常会在其中放置活动，例如在中 <xref:System.Activities.Statements.Sequence> 。 删除活动设计器将创建一个 <xref:System.Activities.Statements.InvokeDelegate> 活动，其默认值为 <xref:System.Activities.Activity.DisplayName%2A> InvokeDelegate。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **InvokeDelegate** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate 属性

下表列出 <xref:System.Activities.Statements.InvokeDelegate> 属性并说明如何在设计器中使用它们。 这些属性可在属性网格中进行编辑，某些属性可以在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.InvokeDelegate> 活动的友好名称。 默认值为 InvokeDelegate。<br /><br /> 尽管 <xref:System.Activities.Activity.DisplayName%2A> 不是严格需要的，但最好使用一个。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|正确|要在执行活动时调用的 <xref:System.Activities.ActivityDelegate> 的名称。 此属性可以在设计器图面上进行编辑，并且是必需的。|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|错误|调用委托的参数集合。 键是中的参数对象的名称 <xref:System.Activities.ActivityDelegate> ，值是计算表达式并将其分配给相应参数对象的参数。 若要显示可在其中设置此属性的 " **DelegateArguments** " 对话框，请单击 "属性" 网格的 " **DelegateArguments** " 字段中的省略号按钮。 单击 "**创建自变量**" 字段以添加参数。|

## <a name="see-also"></a>另请参阅

- [如何：在工作流设计器中定义和使用活动委托](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)