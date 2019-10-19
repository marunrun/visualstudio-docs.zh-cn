---
title: 重新引发活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c65469242a60c64d6f31bfaea4fdbbf2d5251a34
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663357"
---
# <a name="rethrow-activity-designer"></a>Rethrow 活动设计器
**再次引发**活动设计器用于创建和配置 <xref:System.Activities.Statements.Rethrow> 活动。

## <a name="the-rethrow-activity"></a>Rethrow 活动
 <xref:System.Activities.Statements.Rethrow> 活动引发先前已引发的异常。 此活动只能在 <xref:System.Activities.Statements.Catch> 活动的 <xref:System.Activities.Statements.TryCatch> 处理程序中使用。

### <a name="using-the-rethrow-activity-designer"></a>使用 ReThrow 活动设计器
 重新**引发**活动设计器可在 "**工具箱**" 的 "**错误处理**" 类别中找到，可通过单击 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 左侧的 "**工具箱**" 选项卡（或者 **，从** **"视图**" 菜单或 CTRL + ALT + X。）

 重新**引发**活动设计器可以从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建一个 <xref:System.Activities.Statements.Rethrow> 活动，其中包含 Throw 的默认**DisplayName** 。 可以在 "重新**抛**出" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A> 值。

### <a name="the-rethrow-properties"></a>Rethrow 属性
 下表列出 <xref:System.Activities.Statements.Rethrow> 属性并说明如何在设计器中使用它们。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Rethrow> 活动的可选友好名称。 默认值为 Rethrow。|

## <a name="see-also"></a>请参阅
 [集合](../workflow-designer/collection-activity-designers.md) [Throw](../workflow-designer/throw-activity-designer.md) [TryCatch](../workflow-designer/trycatch-activity-designer.md)