---
title: 工作流设计器持久活动设计器
description: 了解持续活动，以及如何使用 "持久活动设计器" 创建和配置持久活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Persist.UI
ms.assetid: be8648dd-3eb9-4a50-8ec1-57a8be804692
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3daa7cef76d2448cc7bcda66a967a3406bb2352c
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94435568"
---
# <a name="persist-activity-designer"></a>Persist 活动设计器

" **持久** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.Persist> 活动。

## <a name="the-persist-activity"></a>Persist 活动

<xref:System.Activities.Statements.Persist> 活动用于将工作流保存到磁盘中（如有可能）。 <xref:System.Activities.Statements.Persist> 活动无法在非持久性区域中执行，例如，在 <xref:System.Activities.Statements.TransactionScope> 活动中。 如果在 <xref:System.Activities.Statements.Persist> 非持久性作用域中使用活动，则在运行时将引发异常。

### <a name="using-the-persist-activity-designer"></a>使用 Persist 活动设计器

" **持久** " 活动设计器可在 " **工具箱** " 的 " **运行时** " 类别中找到，单击 **"工具箱** " 选项卡可访问该设计器 (或者，从 " **视图** " 菜单中选择 " **工具箱** " 或按 CTRL + ALT + X。 ) 

可以将 " **持久** " 活动设计器从 " **工具箱** " 拖放到工作流设计器图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 这将创建一个 <xref:System.Activities.Statements.Persist> 活动，其中默认 **DisplayName** 为 "持久"。 <xref:System.Activities.Activity.DisplayName%2A>可以在 " **持久** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

### <a name="the-persist-properties"></a>Persist 属性

下表列出 <xref:System.Activities.Statements.Persist> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性可以在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Persist> 活动的友好名称。 默认值为 Persist。 虽然显示名称不是绝对必需的，但最好使用显示名称。|

## <a name="see-also"></a>另请参阅

- [运行时](../workflow-designer/runtime-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)
