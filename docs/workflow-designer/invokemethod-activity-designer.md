---
title: 工作流设计器 InvokeMethod 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.InvokeMethod.UI
ms.assetid: 15e6efdc-52ca-46d8-9c5e-063f7c8265a6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8660cd82f9d671da3b535ac228e8ce62c875dc07
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593195"
---
# <a name="invokemethod-activity-designer"></a>InvokeMethod 活动设计器

**InvokeMethod**设计器用于创建和配置 <xref:System.Activities.Statements.InvokeMethod> 活动。

## <a name="the-invokemethod-activity"></a>InvokeMethod 活动

<xref:System.Activities.Statements.InvokeMethod> 调用指定对象或类型的公共方法。

### <a name="use-the-invokemethod-activity-designer"></a>使用 InvokeMethod 活动设计器

访问 "**工具箱**" 的 "**基元**" 类别中的 " **InvokeMethod** " 活动设计器。 可以将 " **InvokeMethod** " 活动设计器从 "**工具箱**" 拖放到工作流设计器表面上，通常会在其中放置活动，如 <xref:System.Activities.Statements.Sequence>内。 删除活动设计器将创建一个 <xref:System.Activities.Statements.InvokeMethod> 的活动，其默认 <xref:System.Activities.Activity.DisplayName%2A> 为 InvokeMethod。 可以在 " **InvokeMethod** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。

### <a name="the-invokemethod-properties"></a>InvokeMethod 属性

下表显示 <xref:System.Activities.Statements.InvokeMethod> 属性，并说明如何在设计器中使用它们。 这些属性可在属性网格中进行编辑，某些属性可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.InvokeMethod> 活动的友好名称。 默认值为 InvokeMethod。<br /><br /> 尽管不是严格需要 <xref:System.Activities.Activity.DisplayName%2A>，但最好是使用一个。|
|<xref:System.Activities.Statements.InvokeMethod.MethodName%2A>|True|要在执行活动时调用的方法的名称。 调用的方法必须声明为**公共**的。 此属性可以在设计器图面上进行编辑，并且是必需的。|
|<xref:System.Activities.Statements.InvokeMethod.Parameters%2A>|False|所调用方法的参数集合。 将参数添加到集合中的顺序必须与这些参数在方法签名中出现的顺序相同。 若要显示 "**参数**" 对话框，在其中可以设置此属性，请单击 "属性" 网格的 "**参数**" 字段中的省略号按钮。 单击 "**创建自变量**" 按钮以添加参数。|
|<xref:System.Activities.Statements.InvokeMethod.Result%2A>|False|方法调用的返回值。|
|<xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>|True|指定是否异步调用该方法。 默认值为**False**。|
|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>|False|包含要调用的方法的对象。 此属性可以在设计器图面上进行编辑。<br /><br /> 必须设置 <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 或 <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> 之一。|
|<xref:System.Activities.Statements.InvokeMethod.TargetType%2A>|False|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 的类型。 此属性可以在设计器图面上进行编辑。 只有当调用的方法为静态时，才必须设置此属性。|

若要将参数作为C# **out**参数传递（例如，`Method1(out myParam))`，请使用**outargument<int>** 而不是**InOutArgument**

不能使用 <xref:System.Activities.Statements.InvokeMethod> 活动调用带有名为**TargetObject**或**Result**的参数的方法。 原因是 <xref:System.Activities.Statements.InvokeMethod> 活动在 <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> 中注册 <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>、<xref:System.Activities.Statements.InvokeMethod.Result%2A> 和 <xref:System.Activities.Activity.CacheMetadata%2A>。

在 <xref:System.Activities.Activity.CacheMetadata%2A> 中注册这些参数的算法如下所列：

1. 注册 <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 自变量。

2. 注册 <xref:System.Activities.Statements.InvokeMethod.Result%2A> 自变量。

3. 循环访问 <xref:System.Activities.Statements.InvokeMethod.Parameters%2A> 集合并注册每个自变量。

产生的异常的类型为 <xref:System.Activities.InvalidWorkflowException>，其中包含以下消息："InvokeMethod"：已存在名为 "TargetObject" 的变量、RuntimeArgument 或 DelegateArgument。 在环境作用域中，名称必须唯一。

此限制不适用于 <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> 和 <xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>。 它们不是工作流参数，因此不在 <xref:System.Activities.Activity.CacheMetadata%2A> 方法的 <xref:System.Activities.Statements.InvokeMethod> 活动的 <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> 集合中进行注册。

## <a name="see-also"></a>请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay](../workflow-designer/delay-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)
