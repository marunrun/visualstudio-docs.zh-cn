---
title: Pick 活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 15320289c3f668f2bc0a84d9653110d02536a32e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694501"
---
# <a name="pick-activity-designer"></a>Pick 活动设计器
<xref:System.Activities.Statements.Pick> 活动提供基于事件的控制流。 该活动执行多个分支中的一个分支来响应某个触发的事件。  
  
## <a name="the-pick-activity"></a>Pick 活动  
 <xref:System.Activities.Statements.Pick> 活动包含一个 <xref:System.Activities.Statements.PickBranch> 对象的集合，<xref:System.Activities.Statements.Pick> 活动会由于某些作为触发器的传入事件而执行其中一个对象。 因此，[!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供了基于事件的控制流建模。 每个 <xref:System.Activities.Statements.PickBranch> 都包含一个 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 和一个 <xref:System.Activities.Statements.PickBranch.Action%2A>。 开始执行 <xref:System.Activities.Statements.Pick> 活动时，会安排 <xref:System.Activities.Statements.PickBranch> 元素的所有触发器活动。 在第一个活动完成之后，安排其相应的操作活动，并且取消所有其他触发器活动。  
  
### <a name="how-to-use-the-pick-activity-designer"></a>如何使用 Pick 活动设计器  
 **选取**活动设计器可在**控制流**的类别**工具箱**，这通过单击来访问**工具箱**选项卡上[!INCLUDE[wfd2](../includes/wfd2-md.md)](或者，选择**工具栏**从**视图**菜单或 CTRL + ALT + X。)  
  
 **选取**活动设计器可以从拖动**工具箱**拖放到[!INCLUDE[wfd2](../includes/wfd2-md.md)]图面上活动设计器放置的任何位置通常情况下，示例中的内部**序列**活动设计器。 将该设计器放置到 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中之后，它会创建一个 <xref:System.Activities.Statements.Pick> 活动，默认情况下，该活动包含两个空的 <xref:System.Activities.Statements.PickBranch> 活动，作为显示名称为 Branch1 和 Branch2 的元素。 二者各自<xref:System.Activities.Statements.PickBranch.DisplayName%2A>属性值可以在中编辑**PickBranch**活动设计器标头中或在**属性**窗口为每个分支。  
  
 有两种方法来添加<xref:System.Activities.Statements.PickBranch>活动的集合<xref:System.Activities.Statements.Pick>对象： 拖放**PickBranch**设计器从**工具箱**或通过使用从上下文菜单内**选取**设计图面。 有关详细信息，请参阅[PickBranch](../workflow-designer/pickbranch-activity-designer.md)主题。 请注意的唯一项，可以放置在**选取**活动设计器是**PickBranch**活动设计器。  
  
### <a name="pick-activity-properties-in-the-workflow-designer"></a>工作流设计器中的 Pick 活动属性  
 下表列出 <xref:System.Activities.Statements.Pick> 属性并说明如何在设计器中使用它们。 这些属性可以在属性网格中或设计器图面上进行编辑。  
  
|属性名|必需|用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|指定 <xref:System.Activities.Statements.Pick> 活动设计器在标头中的友好名称。 默认值为 Pick。 可以在属性网格或直接在活动设计器的标头中编辑该值。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|  
  
## <a name="see-also"></a>请参阅  
 [控制流](../workflow-designer/control-flow-activity-designers.md)   
 [Pick 活动](https://msdn.microsoft.com/library/b3e49b7f-0285-4720-8c09-11ae18f0d53e)   
 [使用 Pick 活动](https://msdn.microsoft.com/library/b89be812-a247-4025-b0e3-ffb20db027a6)