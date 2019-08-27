---
title: TerminateWorkflow 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TerminateWorkflow.UI
ms.assetid: 08e632ed-0724-4fb4-9df1-f8d443eaf0ac
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b471cee4a07722e37ae4b58817823dd4fa48ee26
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004427"
---
# <a name="terminateworkflow-activity-designer"></a>TerminateWorkflow 活动设计器
**TerminateWorkflow**活动设计器用于创建和配置<xref:System.Activities.Statements.TerminateWorkflow>活动。  
  
## <a name="the-terminateworkflow-activity"></a>TerminateWorkflow 活动  
 <xref:System.Activities.Statements.TerminateWorkflow> 活动终止工作流的执行。  
  
### <a name="using-the-terminateworkflow-activity-designer"></a>使用 TerminateWorkflow 活动设计器  
 **TerminateWorkflow**活动设计器可在**运行时**类别**工具箱**，这通过单击来访问**工具箱**选项卡 (或者，选择**工具箱**从**视图**菜单或 CTRL + ALT + X。)  
  
 **TerminateWorkflow**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上任何位置通常放置活动的例如内<xref:System.Activities.Statements.Sequence>。 这将创建<xref:System.Activities.Statements.TerminateWorkflow>默认值的活动**DisplayName** TerminateWorkflow。 <xref:System.Activities.Activity.DisplayName%2A>可以在的标头中编辑**TerminateWorkflow**活动设计器中或在**DisplayName**属性网格的框。  
  
### <a name="the-terminateworkflow-properties"></a>TerminateWorkflow 属性  
 下表列出 <xref:System.Activities.Statements.TerminateWorkflow> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中进行编辑，其中一些属性还可以在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 图面上进行编辑。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.TerminateWorkflow> 活动的友好名称。 默认值为 TerminateWorkflow。 虽然显示名称不是绝对必需的，但最好使用显示名称。|  
|<xref:System.Activities.Statements.TerminateWorkflow.Exception%2A>|False|终止工作流时要引发的异常。 此属性在属性网格中设置。|  
|<xref:System.Activities.Statements.TerminateWorkflow.Reason%2A>|False|解释终止工作流的原因。 此属性在属性网格中设置。|  
  
## <a name="see-also"></a>请参阅  
 [运行时](../workflow-designer/runtime-activity-designers.md)   
 [Persist](../workflow-designer/persist-activity-designer.md)