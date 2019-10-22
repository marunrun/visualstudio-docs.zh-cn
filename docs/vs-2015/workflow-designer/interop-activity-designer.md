---
title: 互操作活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 994d7776ff7c32f8dd309e667597550637ef2b5a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659036"
---
# <a name="interop-activity-designer"></a>Interop 活动设计器
" **Interop** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.Interop> 活动。

## <a name="the-interop-activity"></a>Interop 活动
 <xref:System.Activities.Statements.Interop> 活动管理从工作流中的 <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> 派生的活动类型的执行。

### <a name="using-the-interop-activity-designer"></a>使用 Interop 活动设计器
 **互操作**活动设计器可在 "**工具箱**" 的 "**迁移**" 类别中找到，可通过单击 "**工具箱**" 选项卡（或者，从 "**视图**" 菜单中选择 "**工具箱**" 或按 CTRL + ALT + X 来访问）。

 如果项目面向的是完整 [!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)]，则包含 <xref:System.Activities.Statements.Interop> 活动的[迁移](../workflow-designer/migration-activity-designers.md)类别仅显示在**工具箱**中。

 对于C#项目，可以通过右键单击**解决方案资源管理器**中的项目并选择 "**属性**"，重新将项目定位为使用完整 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]。 在 "**应用程序**" 选项卡上，选择**目标框架**中的**NET Framework 4**选项。 选择 "**目标框架更改**" 对话框中的 **"是"** 按钮，该对话框会询问您确认此更改。

 对于 VB 项目，您可以通过右键单击**解决方案资源管理器**中的项目并选择 "**属性**"，重新将项目定位为使用完整 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]。 在 "**编译**" 选项卡上，单击 "**高级编译选项**" 按钮。 从 "**目标框架" 列表**中选择 " **.net Framework 4** "，然后单击 **"确定"** 。 单击 "**目标框架更改**" 对话框中的 **"是"** 按钮，该对话框会询问您确认此更改。

 可以将 " **Interop** " 活动设计器从 "**工具箱**" 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，如 <xref:System.Activities.Statements.Sequence> 内。 这将创建一个具有互操作的默认**DisplayName**的 <xref:System.Activities.Statements.Interop> 活动。 可以在 " **Interop** " 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑 <xref:System.Activities.Activity.DisplayName%2A>。

 单击 "**单击以浏览 ..."** 在 " **Interop** " 活动设计器或属性网格中，" **ActivityType** " 框中的文本将显示 "**浏览并选择 .net 类型**" 对话框。 仅显示工作流 3.0 或工作流 3.5 活动的类型（即仅显示从 <xref:System.Workflow.ComponentModel.Activity> 派生的类型）。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此框指定类型，请参见[浏览和选择 .Net 类型对话框](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md)主题。

### <a name="the-interop-properties"></a>Interop 属性
 下表列出 <xref:System.Activities.Statements.Interop> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑。

|属性名|必需|用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Interop> 活动的友好名称。 默认值为 Interop。 虽然显示名称不是绝对必需的，但最好使用显示名称。|
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|True|指定 <xref:System.Activities.Statements.Interop> 活动包含的活动类型。 指定的此类型必须派生自 <xref:System.Workflow.ComponentModel.Activity>。|

## <a name="see-also"></a>请参阅
 [迁移](../workflow-designer/migration-activity-designers.md)