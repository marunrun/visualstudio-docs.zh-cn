---
title: 工作流设计器-如何：向工作流添加注释
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 2e8f53e162360c7a43df9f0aedda3ff6ef0e6dba
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114414"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>如何：在工作流设计器中给工作流添加备注

为方便创建更大、更复杂的工作流，.NET Framework 4.5 允许开发人员在设计器中向以下类型的项添加批注：

- <xref:System.Activities.Activity>

- <xref:System.Activities.Statements.State>

- <xref:System.Activities.Statements.Transition>

- 从 <xref:System.Activities.Statements.FlowNode> 中派生的类

- <xref:System.Activities.Variable>

- <xref:System.Activities.Argument>

> [!IMPORTANT]
> 批注的内容作为纯文本保存到与工作流关联的 XAML 文件，并可能被其他人读取。 将敏感信息输入批注时要谨慎。

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>在设计器中将批注添加到活动

1. 在工作流设计器中，右键单击工作流设计器中的项，然后选择 "**批注**"、"**添加批注**"。

1. 在提供的空白处添加批注的文本。

   该项显示批注图标。 将鼠标悬停在批注图标上将显示批注的文本。

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>在活动设计器中显示批注

1. 对于在活动外部显示批注的活动设计器，请单击批注装饰器中的**固定**图标。

   批注将显示在活动的设计器中。 在下面的屏幕快照中，活动设计器中显示批注“工作流中的开始活动”。

   ![活动设计器中显示的注释](../workflow-designer/media/annotationindesigner.png)

2. 若要在活动设计器外显示批注，请将鼠标悬停在活动设计器中的批注区域上方，并单击 "**取消固定**" 图标

   ![在活动的设计器外部显示的批注](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>显示或隐藏所有批注

1. 右键单击一个有批注的活动。 选择 "**批注**"，**显示所有批注**。

   所有批注都显示在活动的设计器中。

1. 若要显示活动设计器外部的所有批注，请右键单击该活动，然后选择 "**批注**"，**隐藏所有批注**。

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>编辑或删除活动的批注

1. 右键单击一个有批注的活动。

1. 选择 "**批注**"、"**编辑批注**" 或 "**删除批注**"。

   将打开批注以进行编辑或删除。

1. 若要一次删除所有批注，请右键单击工作流设计器，然后选择 "**批注**"，**删除所有批注**。

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>添加、编辑和删除变量或参数的批注

1. 右键单击某个变量或参数，然后选择“添加批注”。

1. 输入批注的文本。 变量或参数显示批注图标。

1. 右键单击有批注的某个变量或参数。 选择“编辑批注”。

   将打开批注以进行编辑。

1. 右键单击有批注的某个变量或参数。 选择“删除批注”。

   批注将被删除。
