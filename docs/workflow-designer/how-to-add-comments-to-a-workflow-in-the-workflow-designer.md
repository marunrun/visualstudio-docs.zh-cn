---
title: 工作流设计器-如何：将注释添加到工作流
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: c7eb15c6d19ab40df6913dd67466dc20012492b7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62950394"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>如何：在工作流设计器中向工作流添加注释

为方便创建更大、 更复杂的工作流，.NET Framework 4.5，开发人员可将批注添加到以下类型的设计器中的项：

- <xref:System.Activities.Activity>

- <xref:System.Activities.Statements.State>

- <xref:System.Activities.Statements.Transition>

- 从 <xref:System.Activities.Statements.FlowNode> 中派生的类

- <xref:System.Activities.Variable>

- <xref:System.Activities.Argument>

> [!IMPORTANT]
> 批注的内容作为纯文本保存到与工作流关联的 XAML 文件，并可能被其他人读取。 将敏感信息输入批注时要谨慎。

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>在设计器中将批注添加到活动

1. 在工作流设计器中，右键单击设计器，并选择工作流中的项**批注**，**添加批注**。

1. 在提供的空白处添加批注的文本。

   项将显示批注图标。 将鼠标悬停在批注图标上显示批注的文本。

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>在活动设计器中显示批注

1. 与活动设计器，它具有批注显示在活动外，单击**Pin**中批注装饰器图标。

   该批注显示在活动的设计器中。 在下面的屏幕快照中，活动设计器中显示批注“工作流中的开始活动”。

   ![活动设计器中显示的注释](../workflow-designer/media/annotationindesigner.png)

2. 若要显示的批注之外的活动设计器，请将鼠标悬停在活动的设计器中的批注区域，然后单击**Unpin**图标

   ![活动的设计器外显示批注](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>显示或隐藏所有批注

1. 右键单击一个有批注的活动。 选择**批注**，**显示所有批注**。

   在活动的设计器中显示的所有批注。

1. 若要显示的活动设计器之外的所有注释，请右键单击该活动并选择**批注**，**隐藏所有批注**。

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>编辑或删除活动的批注

1. 右键单击一个有批注的活动。

1. 选择**批注**，**编辑批注**或**删除批注**。

   打开以进行编辑或删除批注。

1. 若要同时删除所有批注，请右键单击工作流设计器，然后选择**批注**，**都删除所有批注**。

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>添加、编辑和删除变量或参数的批注

1. 右键单击某个变量或参数，然后选择“添加批注”。

1. 输入批注的文本。 变量或参数显示的批注图标。

1. 右键单击有批注的某个变量或参数。 选择“编辑批注”。

   批注打开以进行编辑。

1. 右键单击有批注的某个变量或参数。 选择“删除批注”。

   删除批注。