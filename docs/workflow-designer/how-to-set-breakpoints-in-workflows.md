---
title: 工作流设计器-如何：在工作流中设置断点
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e41b21c9-c061-4358-8e2f-eb5e412864a8
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9530e7ec018a89c3648f61660a5651eddaace805
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817484"
---
# <a name="how-to-set-breakpoints-in-workflows"></a>如何：在工作流中设置断点

使用工作流设计器时，可以像在 Visual Basic 或 c # 代码中那样在图形工作流上设置断点。 正如所料，工作流执行将在设置的每个断点处停止。

断点具有三种状态： "*挂起*"、"*绑定*" 和 "*错误*"。 当您设置断点时，断点处于“挂起”状态，并且由一个实心的红色图标表示。 当运行时加载了工作流类型后，断点将成为“绑定”状态。 如果为断点指定了不正确的格式（例如无效的活动名称），则会显示一个错误窗口。 断点仍然会添加到断点窗口，但标有一个小“x”。

> [!NOTE]
> 不支持在调用的工作流上设置断点。

> [!NOTE]
> 在调试之前，请确保在 "**工具**选项" "调试" 菜单中选择 "**启用仅我的代码（仅限托管）** " 选项  >  **Options**  >  **Debugging** 。 如果未选择该选项，并且在另一个序列内嵌套了两个序列，并且在第一个内部序列上设置了一个断点，则按**F11**不会调试到第二个内部序列中。

> [!NOTE]
> 如果 XAML 文件属性的完整路径不准确，则不会命中工作流中的断点。 将项目或解决方案移到另一个文件夹或另一台计算机后，XAML 文件的完整路径不准确。 选择**Ctrl** + **S** ，保存并更新 "完整路径" 属性。

## <a name="to-set-a-breakpoint-on-an-activity-in-the-design-view"></a>在设计视图中的活动上设置断点

1. 选择希望调试器在其上中断的活动。

2. 在 "**调试**" 菜单上，选择 "**切换断点**"。 此时将在该活动的左上边缘显示一个红色图标。

   另外，还可以在选择活动后按**F9** ，或右键单击该活动，然后**Breakpoint**  >  从右键菜单中选择 "断点" "**插入断点**"。

## <a name="see-also"></a>请参阅

- [使用工作流设计器调试工作流](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)
- [如何：使用工作流设计器调试 XAML](../workflow-designer/how-to-debug-xaml-with-the-workflow-designer.md)
