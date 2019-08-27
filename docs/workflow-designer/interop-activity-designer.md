---
title: 工作流设计器的 Interop 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 688ef92fae5bd0cbaa5ddc653bbaab5692f4827f
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747140"
---
# <a name="interop-activity-designer"></a>Interop 活动设计器

**Interop**活动设计器用于创建和配置<xref:System.Activities.Statements.Interop>活动。

## <a name="the-interop-activity"></a>Interop 活动

<xref:System.Activities.Statements.Interop> 活动管理从工作流中的 <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> 派生的活动类型的执行。

### <a name="use-the-interop-activity-designer"></a>使用 Interop 活动设计器

**互操作**活动设计器可在**迁移**类别**工具箱**，这通过单击来访问**工具箱**选项卡。或者，选择**工具箱**从**视图**菜单中或按**Ctrl**+**Alt** + **X**。

[迁移](../workflow-designer/migration-activity-designers.md)包含的类别<xref:System.Activities.Statements.Interop>活动才会显示在**工具箱**如果项目面向.NET Framework 4 （完整） 或更高版本。 如果有必要，您可以更改的 framework 版本的项目目标。

**互操作**活动设计器可以从拖动**工具箱**和放置到工作流设计器图面上通常放置活动的例如内无论<xref:System.Activities.Statements.Sequence>。 删除**Interop**活动设计器创建<xref:System.Activities.Statements.Interop>默认值的活动**DisplayName**互操作。 可以编辑<xref:System.Activities.Activity.DisplayName%2A>中的标头**互操作**活动设计器中，或在**DisplayName**属性网格的框。

单击**单击此项可浏览**中的文本**ActivityType**框中上,**互操作**活动设计器或在属性网格中，若要打开**浏览和选择.Net 类型**对话框。 显示的工作流 3.0 或工作流 3.5 活动的唯一类型。 也就是说，只有类型派生自<xref:System.Workflow.ComponentModel.Activity>显示。 有关使用此框以指定类型的详细信息，请参阅[浏览并选择.NET 类型对话框](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md)。

### <a name="the-interop-properties"></a>Interop 属性

下表显示<xref:System.Activities.Statements.Interop>属性，并说明如何在设计器中使用。 在属性网格中或在工作流设计器图面上，可以编辑这些属性。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Interop> 活动的友好名称。 默认值是**互操作**。 虽然显示名称不是必需的它建议提供一个。|
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|True|指定 <xref:System.Activities.Statements.Interop> 活动包含的活动类型。 指定的此类型必须派生自 <xref:System.Workflow.ComponentModel.Activity>。|

## <a name="see-also"></a>请参阅

- [迁移](../workflow-designer/migration-activity-designers.md)