---
title: Interop 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 55829e85b17bcdc70e419a8496d4756d0acb4a56
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952043"
---
# <a name="interop-activity-designer"></a>Interop 活动设计器
**Interop**活动设计器用于创建和配置<xref:System.Activities.Statements.Interop>活动。  
  
## <a name="the-interop-activity"></a>Interop 活动  
 <xref:System.Activities.Statements.Interop> 活动管理从工作流中的 <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> 派生的活动类型的执行。  
  
### <a name="using-the-interop-activity-designer"></a>使用 Interop 活动设计器  
 **互操作**活动设计器可在**迁移**类别**工具箱**，这通过单击来访问**工具箱**选项卡 (或者，选择**工具箱**从**视图**菜单或 CTRL + ALT + X。)  
  
 [迁移](../workflow-designer/migration-activity-designers.md)包含的类别<xref:System.Activities.Statements.Interop>活动中仅出现**工具箱**如果你的项目面向完整[!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)]。  
  
 对于 C# 项目，您可以重新将项目定为使用完整[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]右键单击该项目中的**解决方案资源管理器**，然后选择**属性**。 上**应用程序**选项卡上，选择**NET Framework 4**选项**目标框架**。 选择**是**按钮**目标框架更改**显示请求您确认此更改的对话框。  
  
 对于 VB 项目，您可以重新将项目定为使用完整[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]项目中，右键单击**解决方案资源管理器**，然后选择**属性**。 上**编译**选项卡上，单击**高级编译选项**按钮。 选择 **.Net Framework 4**从**目标框架列表**，然后单击**确定**。 单击**是**按钮**目标框架更改**显示请求您确认此更改的对话框。  
  
 **Interop**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的例如内<xref:System.Activities.Statements.Sequence>。 这将创建<xref:System.Activities.Statements.Interop>默认值的活动**DisplayName**互操作。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**互操作**活动设计器中或在**DisplayName**属性网格的框。  
  
 单击**单击此项可浏览...** 中的文本**ActivityType**框中上,**互操作**活动设计器或在属性网格中，以显示**浏览并选择.Net 类型**对话框。 仅显示工作流 3.0 或工作流 3.5 活动的类型（即仅显示从 <xref:System.Workflow.ComponentModel.Activity> 派生的类型）。 [!INCLUDE[crabout](../includes/crabout-md.md)] 使用此框以指定类型，请参阅[浏览并选择.NET 类型对话框](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md)主题。  
  
### <a name="the-interop-properties"></a>Interop 属性  
 下表列出 <xref:System.Activities.Statements.Interop> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Interop> 活动的友好名称。 默认值为 Interop。 虽然显示名称不是绝对必需的，但最好使用显示名称。|  
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|True|指定 <xref:System.Activities.Statements.Interop> 活动包含的活动类型。 指定的此类型必须派生自 <xref:System.Workflow.ComponentModel.Activity>。|  
  
## <a name="see-also"></a>请参阅  
 [迁移](../workflow-designer/migration-activity-designers.md)