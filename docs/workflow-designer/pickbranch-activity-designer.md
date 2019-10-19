---
title: 工作流设计器 PickBranch 活动设计器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.PickBranch.UI
ms.assetid: f523ad47-bbc0-4cda-a35c-41e67c4ba081
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a43fa99c9f5fe4fbb3cfe336efb983fced655f2a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650058"
---
# <a name="pickbranch-activity-designer"></a>PickBranch 活动设计器

<xref:System.Activities.Statements.PickBranch> 在可由传入事件触发的 <xref:System.Activities.Statements.Pick> 活动中提供基于事件的执行路径。

## <a name="pickbranch"></a>PickBranch

<xref:System.Activities.Statements.PickBranch> 对象包含在 <xref:System.Activities.Statements.Pick.Branches%2A> 活动的 <xref:System.Activities.Statements.Pick> 集合中。 每个 <xref:System.Activities.Statements.PickBranch> 都包含在 <xref:System.Activities.Statements.Pick> 活动的一个分支中，并可因某些用作触发器的传入事件而执行。 通过这种方式，工作流设计器提供基于事件的控制流建模。 每个 <xref:System.Activities.Statements.PickBranch> 都包含一个 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 和一个 <xref:System.Activities.Statements.PickBranch.Action%2A>。

### <a name="how-to-use-the-pick-activity-designer"></a>如何使用 Pick 活动设计器

访问 "**工具箱**" 的 "**控制流**" 类别中的 " **PickBranch** " 设计器。

默认情况下，显示名称为**Branch1**和**Branch2**的两个空 <xref:System.Activities.Statements.PickBranch> 对象作为 <xref:System.Activities.Statements.Pick> 活动的元素创建（当**Pick**活动设计器最初拖到工作流设计器上时）。 可以在**PickBranch**设计器标头或每个分支的 "**属性**" 窗口中编辑这些各自 <xref:System.Activities.Statements.PickBranch.DisplayName%2A> 属性值。

可通过两种方法将 <xref:System.Activities.Statements.PickBranch> 对象添加到 <xref:System.Activities.Statements.Pick> 对象的集合：从**工具箱**中拖放**PickBranch**设计器，或使用**Pick**设计图面中的右键单击菜单：

- 将**PickBranch**设计器从 "**工具箱**" 拖放到工作流设计器图面上的 " **Pick** " 活动设计器的某个分支中时，将创建一个 <xref:System.Activities.Statements.PickBranch>。 新 <xref:System.Activities.Statements.PickBranch> 对象可放置在 <xref:System.Activities.Statements.Pick> 设计器内已包含在集合中的任何现有 <xref:System.Activities.Statements.PickBranch> 元素的左侧或右侧。 使用鼠标将**PickBranch**设计器拖到 " **pick** " 设计器上时， **Pick**设计器会使用一个垂直的蓝灰条来指示在给定鼠标位置添加 <xref:System.Activities.Statements.PickBranch> 的位置。

- 右键单击 "**选择**活动设计器（但不在**PickBranch**设计器内）" 以获取上下文菜单并选择 "**创建分支**" 以添加新的 <xref:System.Activities.Statements.PickBranch>。 请注意，新 <xref:System.Activities.Statements.PickBranch> 将添加到 " **Pick**设计器" 中现有 <xref:System.Activities.Statements.PickBranch> 对象的右侧。

可以通过单击其标头右侧的双插入符号，展开**PickBranch**设计器，以显示**触发器**和**操作**框或折叠。 通过将活动拖放到设计器的 "**触发器**" 和 "**操作**" 框中，编辑每个 <xref:System.Activities.Statements.PickBranch> 的 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 和 <xref:System.Activities.Statements.PickBranch.Action%2A>。

可以通过将对象拖放到**Pick**设计器中的新位置来重新排序 <xref:System.Activities.Statements.Pick> 对象 <xref:System.Activities.Statements.Pick.Branches%2A> 集合中的 <xref:System.Activities.Statements.PickBranch> 对象。 **Pick**设计器使用垂直的蓝灰色区段来指示在给定鼠标位置添加 <xref:System.Activities.Statements.PickBranch> 的位置。

有两种方法可删除 <xref:System.Activities.Statements.PickBranch>：

- 选择**PickBranch**设计器并将其删除。
- 选择**PickBranch**设计器，右键单击以获取上下文菜单，然后选择 "**删除**"。

请确保选择 " **PickBranch** " 设计器，因为在其**触发器**或**操作**框中选择某个活动时出错，会删除这些活动之一，而不是删除 <xref:System.Activities.Statements.PickBranch> 的对象。

### <a name="pickbranch-properties-in-the-workflow-designer"></a>工作流设计器中的 PickBranch 属性

下表显示最有用的 <xref:System.Activities.Statements.PickBranch> 属性，并介绍如何在工作流设计器中使用它们。

|属性名|必需|用法|
|-|--------------|-|
|<xref:System.Activities.Statements.PickBranch.DisplayName%2A>|False|在**PickBranch**设计器的标头中显示的友好名称。 默认值为 Branch。<br /><br /> 虽然 <xref:System.Activities.Activity.DisplayName%2A> 不是绝对必需的，但最好使用该属性。|
|<xref:System.Activities.Statements.PickBranch.Trigger%2A>|True|每个 <xref:System.Activities.Statements.PickBranch> 都包含一个可调用 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 的 <xref:System.Activities.Statements.PickBranch.Action%2A> 操作。|
|<xref:System.Activities.Statements.PickBranch.Action%2A>|False|每个 <xref:System.Activities.Statements.PickBranch> 都包含一个触发时将执行的 <xref:System.Activities.Statements.PickBranch.Action%2A>。|

## <a name="see-also"></a>请参阅

- [控制流](../workflow-designer/control-flow-activity-designers.md)
- [Pick 活动](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [使用 Pick 活动](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)