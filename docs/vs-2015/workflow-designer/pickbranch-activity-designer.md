---
title: PickBranch 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.PickBranch.UI
ms.assetid: f523ad47-bbc0-4cda-a35c-41e67c4ba081
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c47e893cfe84c984231891583abe5d0fea0178dc
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694468"
---
# <a name="pickbranch-activity-designer"></a>PickBranch 活动设计器
<xref:System.Activities.Statements.PickBranch> 在可由传入事件触发的 <xref:System.Activities.Statements.Pick> 活动中提供基于事件的执行路径。  
  
## <a name="pickbranch"></a>PickBranch  
 <xref:System.Activities.Statements.PickBranch> 对象包含在 <xref:System.Activities.Statements.Pick.Branches%2A> 活动的 <xref:System.Activities.Statements.Pick> 集合中。 每个 <xref:System.Activities.Statements.PickBranch> 都包含在 <xref:System.Activities.Statements.Pick> 活动的一个分支中，并可因某些用作触发器的传入事件而执行。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 由此提供基于事件的控制流建模。 每个 <xref:System.Activities.Statements.PickBranch> 都包含一个 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 和一个 <xref:System.Activities.Statements.PickBranch.Action%2A>。  
  
### <a name="how-to-use-the-pick-activity-designer"></a>如何使用 Pick 活动设计器  
 **PickBranch**设计器可在**控制流**类别**工具箱**，这通过单击来访问**工具箱**选项卡上[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X)。  
  
 两个空<xref:System.Activities.Statements.PickBranch>的对象显示名称**Branch1**和**分支 2**默认情况下创建的元素作为<xref:System.Activities.Statements.Pick>活动时**选取**活动设计器最初放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]。 二者各自<xref:System.Activities.Statements.PickBranch.DisplayName%2A>属性值可以在中编辑**PickBranch**设计器标头中或在**属性**窗口为每个分支。  
  
 有两种方法来添加<xref:System.Activities.Statements.PickBranch>对象的集合<xref:System.Activities.Statements.Pick>对象： 拖放**PickBranch**设计器从**工具箱**或通过使用从上下文菜单内**选取**设计图面：  
  
1. **PickBranch**设计器创建<xref:System.Activities.Statements.PickBranch>时从拖动**工具箱**放到的分支之一**选取**上的活动设计器[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面。 新 <xref:System.Activities.Statements.PickBranch> 对象可放置在 <xref:System.Activities.Statements.Pick> 设计器内已包含在集合中的任何现有 <xref:System.Activities.Statements.PickBranch> 元素的左侧或右侧。 当拖动**PickBranch**拖动到设计器**选取**用鼠标，设计器**选取**设计器使用一个垂直的蓝灰条来指示何处<xref:System.Activities.Statements.PickBranch>添加作为给定的鼠标放置位置。  
  
2. 右键单击**选取**活动设计器 (但不是能在**PickBranch**设计器) 获取上下文菜单并选择**创建分支**来添加新<xref:System.Activities.Statements.PickBranch>。 请注意，新<xref:System.Activities.Statements.PickBranch>添加到现有右侧<xref:System.Activities.Statements.PickBranch>中的对象**选取**设计器。  
  
   **PickBranch**设计器可展开以显示**触发器**并**操作**框或通过单击其标头右侧的双插入符号折叠。 编辑<xref:System.Activities.Statements.PickBranch.Trigger%2A>并<xref:System.Activities.Statements.PickBranch.Action%2A>每个<xref:System.Activities.Statements.PickBranch>通过将活动放入**触发器**并**操作**及其设计器的框。  
  
   <xref:System.Activities.Statements.PickBranch>中的对象<xref:System.Activities.Statements.Pick.Branches%2A>系列<xref:System.Activities.Statements.Pick>对象，可以通过拖放到中的新位置重新排序**选取**设计器。 **选取**设计器使用一个垂直的蓝灰条来指示何处<xref:System.Activities.Statements.PickBranch>添加作为给定的鼠标放置位置。  
  
   有两种方法可删除 <xref:System.Activities.Statements.PickBranch>：  
  
3. 选择**PickBranch**设计器并将其删除。  
  
4. 选择**PickBranch**设计器中，右键单击以获取上下文菜单并选择**删除**。  
  
   请务必选择**PickBranch**设计器中，选择其中一个内的活动作为其**触发器**或**操作**框错误地删除这些活动之一，而不<xref:System.Activities.Statements.PickBranch>对象。  
  
### <a name="pickbranch-properties-in-the-workflow-designer"></a>工作流设计器中的 PickBranch 属性  
 下表列出最有用的 <xref:System.Activities.Statements.PickBranch> 属性并说明如何在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中使用它们。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.PickBranch.DisplayName%2A>|False|标头中显示的友好名称**PickBranch**设计器。 默认值为 Branch。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|  
|<xref:System.Activities.Statements.PickBranch.Trigger%2A>|True|每个 <xref:System.Activities.Statements.PickBranch> 都包含一个可调用 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 的 <xref:System.Activities.Statements.PickBranch.Action%2A> 操作。|  
|<xref:System.Activities.Statements.PickBranch.Action%2A>|False|每个 <xref:System.Activities.Statements.PickBranch> 都包含一个触发时将执行的 <xref:System.Activities.Statements.PickBranch.Action%2A>。|  
  
## <a name="see-also"></a>请参阅  
 [控制流](../workflow-designer/control-flow-activity-designers.md)   
 [Pick 活动](https://msdn.microsoft.com/library/b3e49b7f-0285-4720-8c09-11ae18f0d53e)   
 [使用 Pick 活动](https://msdn.microsoft.com/library/b89be812-a247-4025-b0e3-ffb20db027a6)