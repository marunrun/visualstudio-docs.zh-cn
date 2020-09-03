---
title: 持久活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Persist.UI
ms.assetid: be8648dd-3eb9-4a50-8ec1-57a8be804692
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 60a63dd4036863641646e85a89f5018cba786802
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672624"
---
# <a name="persist-activity-designer"></a>Persist 活动设计器
" **持久** " 活动设计器用于创建和配置 <xref:System.Activities.Statements.Persist> 活动。

## <a name="the-persist-activity"></a>Persist 活动
 <xref:System.Activities.Statements.Persist> 活动用于将工作流保存到磁盘中（如有可能）。 <xref:System.Activities.Statements.Persist> 活动无法在非持久性区域中执行，例如，在 <xref:System.Activities.Statements.TransactionScope> 活动中。 如果在非持久性作用域中使用 <xref:System.Activities.Statements.Persist> 活动，则在运行时会引发异常。

### <a name="using-the-persist-activity-designer"></a>使用 Persist 活动设计器
 "**持久**" 活动设计器可在 "**工具箱**" 的 "**运行时**" 类别中找到，单击 **"工具箱**" 选项卡可访问该设计器 (或者，从 "**视图**" 菜单中选择 "**工具箱**" 或按 CTRL + ALT + X。 ) 

 可以将 " **持久** " 活动设计器从 " **工具箱** " 拖放到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上通常放置活动的任何位置，例如中 <xref:System.Activities.Statements.Sequence> 。 这将创建一个 <xref:System.Activities.Statements.Persist> 活动，其中默认 **DisplayName** 为 "持久"。 <xref:System.Activities.Activity.DisplayName%2A>可以在 "**持久**" 活动设计器的标头中或在属性网格的 " **DisplayName** " 框中编辑。

### <a name="the-persist-properties"></a>Persist 属性
 下表列出 <xref:System.Activities.Statements.Persist> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑。

|属性名称|必选|使用情况|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|错误|<xref:System.Activities.Statements.Persist> 活动的友好名称。 默认值为 Persist。 虽然显示名称不是绝对必需的，但最好使用显示名称。|

## <a name="see-also"></a>另请参阅
 [运行时](../workflow-designer/runtime-activity-designers.md) [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)