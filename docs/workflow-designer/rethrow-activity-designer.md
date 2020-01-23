---
title: 工作流设计器-再次引发活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3cb73a674e702d54f970c5dea7ec051f100382c9
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114747"
---
# <a name="rethrow-activity-designer"></a>Rethrow 活动设计器

**再次引发**活动设计器用于创建和配置 <xref:System.Activities.Statements.Rethrow> 活动。

## <a name="the-rethrow-activity"></a>重新引发活动

<xref:System.Activities.Statements.Rethrow> 活动引发先前已引发的异常。 此活动只能在 <xref:System.Activities.Statements.Catch> 活动的 <xref:System.Activities.Statements.TryCatch> 处理程序中使用。

### <a name="use-the-rethrow-activity-designer"></a>使用重新引发活动设计器

访问 "**工具箱**" 的 "**错误处理**" 类别中的重新**抛**活动设计器。 重新**引发**活动设计器可以从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence>内。 删除活动设计器将创建一个 <xref:System.Activities.Statements.Rethrow> 活动，其中包含 Throw 的默认**DisplayName** 。 可以在重新**抛**活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。

### <a name="the-rethrow-properties"></a>重新引发属性

下表显示 <xref:System.Activities.Statements.Rethrow> 属性，并说明如何在设计器中使用这些属性：

|属性名|必需|用量|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Rethrow> 活动的可选友好名称。 默认值为 Rethrow。|

## <a name="see-also"></a>另请参阅

- [收集](../workflow-designer/collection-activity-designers.md)
- [Throw](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)
