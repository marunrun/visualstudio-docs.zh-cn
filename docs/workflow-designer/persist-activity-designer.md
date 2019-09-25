---
title: 工作流设计器持久活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Persist.UI
ms.assetid: be8648dd-3eb9-4a50-8ec1-57a8be804692
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7be70d18b1fc8ff12e2d1fb177b41775954334ed
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254850"
---
# <a name="persist-activity-designer"></a>Persist 活动设计器

"**持久**" 活动设计器用于创建和配置<xref:System.Activities.Statements.Persist>活动。

## <a name="the-persist-activity"></a>Persist 活动

<xref:System.Activities.Statements.Persist> 活动用于将工作流保存到磁盘中（如有可能）。 <xref:System.Activities.Statements.Persist> 活动无法在非持久性区域中执行，例如，在 <xref:System.Activities.Statements.TransactionScope> 活动中。 如果在非持久性作用<xref:System.Activities.Statements.Persist>域中使用活动，则在运行时将引发异常。

### <a name="using-the-persist-activity-designer"></a>使用 Persist 活动设计器

"**持久**" 活动设计器可在 "**工具箱**" 的 "**运行时**" 类别中找到，可通过单击 "**工具箱**" 选项卡（或者，从 "**视图**" 菜单中选择 "**工具箱**" 或按 CTRL + ALT + X 来访问）。

可以将 "**持久**" 活动设计器从 "**工具箱**" 拖放到工作流设计器图面上通常放置活动的任何位置，例如<xref:System.Activities.Statements.Sequence>中。 这将创建<xref:System.Activities.Statements.Persist>一个活动，其中默认**DisplayName**为 "持久"。 可以在 "**持久**" 活动设计器的标头中或在属性网格的 "DisplayName" 框中编辑。 <xref:System.Activities.Activity.DisplayName%2A>

### <a name="the-persist-properties"></a>Persist 属性

下表列出 <xref:System.Activities.Statements.Persist> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性可以在工作流设计器图面上进行编辑。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Persist> 活动的友好名称。 默认值为 Persist。 虽然显示名称不是绝对必需的，但最好使用显示名称。|

## <a name="see-also"></a>请参阅

- [运行时](../workflow-designer/runtime-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)