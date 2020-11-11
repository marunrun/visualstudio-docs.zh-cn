---
title: 工作流设计器中的错误消息
description: 了解处理工作流设计器时可能遇到的错误消息类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- WFDErrorMessages.UI
- System.Activities.Presentation.ErrorActivity.UI
- System.Activities.Presentation.View.ErrorView.UI
ms.assetid: 4d8bbc2e-34fc-477f-9140-4adfd70c34a0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8f3886739cbc6deefd13570ae0f49da7e89ad9b1
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94438030"
---
# <a name="error-messages-in-workflow-designer"></a>工作流设计器中的错误消息

本主题介绍处理工作流设计器时可能遇到的错误消息类型。

## <a name="situations-in-which-errors-in-the-workflow-designer-occur"></a>工作流设计器中出现错误的情况

工作流设计器中的错误在以下情况下发生：

1. 表达式中存在错误。

2. 活动的验证约束未满足。

3. XAML 文件中存在错误，导致活动无法加载。

4. XAML 文件中存在错误，导致工作流无法加载。

无效的表达式和未满足的验证约束不会导致工作流无法生成。 生成工作流会成功，但 <xref:System.Activities.InvalidWorkflowException> 会在运行时引发。 如果 XAML 文件中存在错误，生成将失败。

在 Visual Studio 中，加载工作流时，它的错误将显示在 **错误列表** 中。 若要导航到作为错误源的活动，请在 **错误列表** 中双击错误。

### <a name="expression-errors"></a>表达式错误
 无效表达式用红色圆圈表示，并且该表达式旁有一个白色感叹号。 悬停在此图标上将显示描述错误来源的工具提示。 在 Visual Studio 中，单击表达式以查看显示错误源的行。 悬停在此加下划线的文本上将显示描述错误来源的工具提示。

### <a name="activity-validation-errors"></a>活动验证错误
 活动的验证约束未满足时，红色圆圈及白色感叹号显示在该活动的右上角。 悬停在此图标上将显示描述错误来源的工具提示。

### <a name="xaml-load-errors"></a>XAML 加载错误
 当某个活动无法加载时，将显示一个红色框，其中包含文本 "由于 XAML 中的错误，无法加载活动"。 这通常发生在无法解析活动的类型时。 可以在设计器中删除无效的活动，方法是选中红色框，然后删除它。

### <a name="workflow-load-errors"></a>工作流加载错误
 未能加载工作流时，设计器图面上将显示文本 "工作流设计器遇到的文档问题"，以及导致加载工作流失败的异常信息。 这通常发生在无法分析 XAML 文件时。
