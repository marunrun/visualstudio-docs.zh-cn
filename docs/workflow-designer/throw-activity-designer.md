---
title: 工作流设计器 Throw 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Throw.UI
ms.assetid: 5e97c947-be39-4a1f-af04-000e2e09528a
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fe6a530888c7c28c5c1556114db03a6cd7369fe6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72649850"
---
# <a name="throw-activity-designer"></a>Throw 活动设计器

**Throw**活动设计器用于创建和配置 <xref:System.Activities.Statements.Throw> 活动。

## <a name="the-throw-activity"></a>Throw 活动

<xref:System.Activities.Statements.Throw> 活动会引发一个异常。

### <a name="using-the-throw-activity-designer"></a>使用 Throw 活动设计器

访问 "**工具箱**" 的 "**错误处理**" 类别中的 " **Throw** " 活动设计器。

可以将 " **Throw** " 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建一个 <xref:System.Activities.Statements.Throw> 活动，其中包含 Throw 的默认**DisplayName** 。 可以在 " **Throw** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。 <xref:System.Activities.Statements.Throw.Exception%2A> 属性必须在属性网格上编辑。

### <a name="the-throw-properties"></a>Throw 属性

下表列出 <xref:System.Activities.Statements.Throw> 属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Throw> 活动的可选友好名称。 默认值为 Throw。|
|<xref:System.Activities.Statements.Throw.Exception%2A>|True|要引发的异常。 此异常必须派生自 <xref:System.Exception>。 若要指定此异常，请在属性网格中键入 Visual Basic 表达式。|

## <a name="see-also"></a>请参阅

- [收集](../workflow-designer/collection-activity-designers.md)
- [Rethrow](../workflow-designer/rethrow-activity-designer.md)
- [Throw 活动设计器](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)