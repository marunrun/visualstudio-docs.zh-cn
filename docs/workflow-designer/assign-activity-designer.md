---
title: 工作流设计器分配活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83a01c96b64dcd55adfd775efc266063efbab27d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86875938"
---
# <a name="assign-activity-designer"></a>Assign 活动设计器

" **分配** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.Assign> 活动。

## <a name="the-assign-activity"></a>Assign 活动

<xref:System.Activities.Statements.Assign> 活动为变量或自变量赋值。

### <a name="using-the-assign-activity-designer"></a>使用 Assign 活动设计器

"**分配**" 活动设计器可在 "**工具箱**" 的 "**基元**" 类别中找到，可通过单击 "**工具箱**" 选项卡访问， (或者，从 "**视图**" 菜单中选择 "**工具箱**" 或按 CTRL + ALT + X。 ) 

可以将 " **分配** " 活动设计器从 " **工具箱** " 拖放到所放置活动的工作流设计器表面上，例如中 <xref:System.Activities.Statements.Sequence> 。 删除 " **assign** " 活动设计器将创建一个 <xref:System.Activities.Statements.Assign> 活动，该活动具有 "分配" 的默认 **DisplayName** 。 <xref:System.Activities.Activity.DisplayName%2A>可以在 "**分配**" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

### <a name="the-assign-properties"></a>Assign 属性

下表列出 <xref:System.Activities.Statements.Assign> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性可以在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Assign> 活动的友好名称。 默认值为 Assign。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.Assign.To%2A>|正确|为其赋 <xref:System.Activities.Statements.Assign.Value%2A> 的变量或自变量。 该值必须是有效的 Visual Basic 标识符。 若要设置属性，请在 " **Assign** " 活动设计器或属性网格中的 " **To** " 框中键入 Visual Basic 表达式。|
|<xref:System.Activities.Statements.Assign.Value%2A>|正确|赋给变量的值。 若要设置 <xref:System.Activities.Statements.Assign.Value%2A> ，请在 " **Assign** " 活动设计器或属性网格中的 "**值**" 框中键入 Visual Basic 表达式。|

## <a name="see-also"></a>另请参阅

- [基元](../workflow-designer/primitives-activity-designers.md)
- [延迟](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)