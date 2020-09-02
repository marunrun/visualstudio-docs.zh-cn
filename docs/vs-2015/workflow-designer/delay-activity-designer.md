---
title: 延迟活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a47279bc68503ba645fea3ef23a04ce9d5ef4c41
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656796"
---
# <a name="delay-activity-designer"></a>Delay 活动设计器
" **延迟** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.Delay> 活动。

## <a name="the-delay-activity"></a>Delay 活动
 <xref:System.Activities.Statements.Delay> 活动可将工作流的执行延迟指定时长。

### <a name="using-the-delay-activity-designer"></a>使用 Delay 活动设计器
 "**延迟**" 活动设计器可在 "**工具箱**" 的 "**基元**" 类别中找到，可以通过单击 (的 "**工具箱**" 选项卡访问，也可以 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 从 "**视图**" 菜单中选择 "**工具栏**" 或按 CTRL + ALT + X。 ) 

 可以将 " **延迟** " 活动设计器从 " **工具箱** " 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 这将创建具有 Delay 的默认 <xref:System.Activities.Statements.Delay> 的 <xref:System.Activities.Activity.DisplayName%2A> 活动。 <xref:System.Activities.Activity.DisplayName%2A>可以在 "**延迟**" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

### <a name="the-delay-properties"></a>Delay 属性
 下表列出 <xref:System.Activities.Statements.Delay> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Delay> 活动的友好名称。 默认值为 Delay。 虽然 <xref:System.Activities.Activity.DisplayName%2A> 值不是绝对必需的，但最好使用该属性值。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|正确|将工作流延迟的时长。 此属性在属性网格中设置。 键入 00:00:00 格式的文本 <xref:System.TimeSpan> 或 Visual Basic 表达式来指定时长。|

## <a name="see-also"></a>另请参阅
 [基元](../workflow-designer/primitives-activity-designers.md)[分配](../workflow-designer/assign-activity-designer.md)[延迟活动设计器](../workflow-designer/delay-activity-designer.md) [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md) [WriteLine](../workflow-designer/writeline-activity-designer.md)