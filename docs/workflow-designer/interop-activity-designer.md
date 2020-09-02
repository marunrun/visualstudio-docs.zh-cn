---
title: 工作流设计器-互操作活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8047df3787c0871e369b6079e4f0cc80f6d93949
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72650210"
---
# <a name="interop-activity-designer"></a>Interop 活动设计器

" **Interop** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.Interop> 活动。

## <a name="the-interop-activity"></a>Interop 活动

<xref:System.Activities.Statements.Interop> 活动管理从工作流中的 <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> 派生的活动类型的执行。

### <a name="use-the-interop-activity-designer"></a>使用 Interop 活动设计器

"**互操作**" 活动设计器可在 "**工具箱**" 的 "**迁移**" 类别中找到，可通过单击 "**工具箱**" 选项卡进行访问。或者，从 "**视图**" 菜单中选择 **"工具箱**"，或按**Ctrl** + **Alt** + **X**。

[Migration](../workflow-designer/migration-activity-designers.md) <xref:System.Activities.Statements.Interop> 如果项目面向 .NET Framework 4 (full) 或更高版本，则包含该活动的迁移类别仅显示在**工具箱**中。 如有必要，可以更改项目所面向的框架版本。

可以将 " **互操作** " 活动设计器从 **"工具箱** " 拖放到工作流设计器图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 删除 **interop** 活动设计器将创建一个 <xref:System.Activities.Statements.Interop> 活动，该活动具有 "互操作" 的默认 **DisplayName** 。 您可以在 " <xref:System.Activities.Activity.DisplayName%2A> **Interop** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

单击 " **单击以浏览** " 中的 " **ActivityType** " 框中的文本，在 " **互操作**  " 活动设计器或属性网格中，打开 " **浏览并选择 .net 类型** " 对话框。 仅显示工作流3.0 或工作流3.5 活动的类型。 也就是说，仅显示从派生的类型 <xref:System.Workflow.ComponentModel.Activity> 。 有关使用此框指定类型的详细信息，请参阅 " [浏览并选择 .Net 类型" 对话框](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md)。

### <a name="the-interop-properties"></a>Interop 属性

下表显示了 <xref:System.Activities.Statements.Interop> 这些属性，并介绍了如何在设计器中使用它们。 这些属性可以在属性网格中编辑，也可以在工作流设计器图面上进行编辑。

|属性名称|必选|使用情况|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Interop> 活动的友好名称。 默认值为 **互操作**。 尽管显示名称不是必需的，但建议提供一个。|
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|正确|指定 <xref:System.Activities.Statements.Interop> 活动包含的活动类型。 指定的此类型必须派生自 <xref:System.Workflow.ComponentModel.Activity>。|

## <a name="see-also"></a>另请参阅

- [迁移](../workflow-designer/migration-activity-designers.md)