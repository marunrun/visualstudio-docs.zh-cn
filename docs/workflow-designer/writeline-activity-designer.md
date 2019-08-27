---
title: 工作流设计器-WriteLine 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.WriteLine.UI
ms.assetid: 1b5f29a8-b7fd-477e-949e-2f689cae3c96
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 17dd6e3c617749d82533d8bccb7f0caaa073ac26
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838615"
---
# <a name="writeline-activity-designer"></a>WriteLine 活动设计器

**WriteLine**活动设计器用于创建和配置<xref:System.Activities.Statements.WriteLine>活动。

## <a name="the-writeline-activity"></a>WriteLine 活动

<xref:System.Activities.Statements.WriteLine> 活动将文本写入指定的 <xref:System.IO.TextWriter> 对象。 如果未指定 <xref:System.IO.TextWriter>，则 <xref:System.Activities.Statements.WriteLine> 会将文本写入控制台中。

### <a name="using-the-writeline-activity-designer"></a>使用 WriteLine 活动设计器

访问**WriteLine**中的活动设计器**基元**类别**工具箱**。 **WriteLine**活动设计器可以从拖动**工具箱**只要通常放置活动的例如内放置到工作流设计器图面和<xref:System.Activities.Statements.Sequence>。 这将创建具有 WriteLine 的默认 <xref:System.Activities.Statements.WriteLine> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**WriteLine**活动设计器中或在**DisplayName**属性网格的框。

### <a name="the-writeline-properties"></a>WriteLine 属性

下表列出 <xref:System.Activities.Statements.WriteLine> 属性并说明如何在设计器中使用它们。 可以在属性网格中编辑这些属性，其中一些可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.WriteLine> 活动的友好名称。 默认值为 WriteLine。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.WriteLine.Text%2A>|False|要写入的文本。 若要设置该属性，键入 Visual Basic 表达式**文本**框**WriteLine**活动设计器或在属性网格中。|
|<xref:System.Activities.Statements.WriteLine.TextWriter%2A>|False|<xref:System.IO.TextWriter> 向其写入 <xref:System.Activities.Statements.WriteLine> 的 <xref:System.Activities.Statements.WriteLine.Text%2A>。 默认为控制台。|

## <a name="see-also"></a>请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)