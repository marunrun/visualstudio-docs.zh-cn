---
title: InvokeDelegate | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
caps.latest.revision: 3
author: steved0x
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 30281d8cd5d5ed94ed89a980006f9618292a778d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951965"
---
# <a name="invokedelegate"></a>InvokeDelegate

**InvokeDelegate**设计器用于创建和配置<xref:System.Activities.Statements.InvokeDelegate>活动。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate 活动

<xref:System.Activities.Statements.InvokeDelegate> 调用公共委托。

### <a name="using-the-invokedelegate-activity-designer"></a>使用 InvokeDelegate 活动设计器

**InvokeDelegate**活动设计器可在**基元**类别**工具箱**，这通过单击来访问**工具箱**选项卡[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单中或 CRTL + ALT + X。)

**InvokeDelegate**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的例如内<xref:System.Activities.Statements.Sequence>。 这将创建具有 InvokeDelegate 的默认 <xref:System.Activities.Statements.InvokeDelegate> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**InvokeDelegate**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate 属性

下表列出 <xref:System.Activities.Statements.InvokeDelegate> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 设计器图面上进行编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.InvokeDelegate> 活动的友好名称。 默认值为 InvokeDelegate。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|True|要在执行活动时调用的 <xref:System.Activities.ActivityDelegate> 的名称。 此属性可以在设计器图面上进行编辑。 此属性是强制属性。|
|<<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|False|调用委托的参数集合。 键为 <xref:System.Activities.DelegateArgument> 上的 <xref:System.Activities.ActivityDelegate> 对象的名称，值为其表达式将进行计算并分配给对应 <xref:System.Activities.DelegateArgument> 对象的参数。 在属性网格中，单击中的省略号按钮**DelegateArguments**字段中，它将显示**DelegateArguments**对话框以便您设置此属性。 单击**创建自变量**字段以添加自变量。|

## <a name="see-also"></a>请参阅

- [如何：在工作流设计器中定义和使用活动委托](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)