---
title: Throw 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Throw.UI
ms.assetid: 5e97c947-be39-4a1f-af04-000e2e09528a
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1855daa5016241fb6eb04f05d7218e02083fc0a8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655162"
---
# <a name="throw-activity-designer"></a>Throw 活动设计器
**Throw**活动设计器用于创建和配置 <xref:System.Activities.Statements.Throw> 活动。

## <a name="the-throw-activity"></a>Throw 活动
 <xref:System.Activities.Statements.Throw> 活动会引发一个异常。

### <a name="using-the-throw-activity-designer"></a>使用 Throw 活动设计器
 " **Throw** " 活动设计器可在 "**工具箱**" 的 "**错误处理**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 左侧的 "**工具箱**" 选项卡进行访问（或者，也可以从视图中选择 "**工具栏**"菜单，或按 CTRL + ALT + X。）

 可以将 " **Throw** " 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建一个 <xref:System.Activities.Statements.Throw> 活动，其中包含 Throw 的默认**DisplayName** 。 可以在 " **Throw** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。 <xref:System.Activities.Statements.Throw.Exception%2A> 属性必须在属性网格上编辑。

### <a name="the-throw-properties"></a>Throw 属性
 下表列出 <xref:System.Activities.Statements.Throw> 属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Throw> 活动的可选友好名称。 默认值为 Throw。|
|<xref:System.Activities.Statements.Throw.Exception%2A>|True|要引发的异常。 此异常必须派生自 <xref:System.Exception>。 若要指定此异常，请在属性网格中键入 Visual Basic 表达式。|

## <a name="see-also"></a>请参阅
 [集合](../workflow-designer/collection-activity-designers.md)[再次](../workflow-designer/rethrow-activity-designer.md)[引发 Throw 活动设计器](../workflow-designer/throw-activity-designer.md) [TryCatch](../workflow-designer/trycatch-activity-designer.md)