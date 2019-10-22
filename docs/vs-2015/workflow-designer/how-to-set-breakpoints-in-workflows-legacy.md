---
title: 如何：在工作流中设置断点（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- breakpoints, setting in workflows
- debugging, setting breakpoints in workflows
- debugging workflows, setting breakpoints
- workflows, setting breakpoints
ms.assetid: 78e0be39-3e99-487c-bfef-19db0daf6f42
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 182f28a2b21ae3129ce0d34fae97280ba0a07218
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603592"
---
# <a name="how-to-set-breakpoints-in-workflows-legacy"></a>如何：在工作流中设置断点（旧版）
本主题介绍如何在使用旧 [!INCLUDE[wf](../includes/wf-md.md)] 生成的 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 应用程序中设置断点。 在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 应用程序需要面向 [!INCLUDE[wf2](../includes/wf2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 当使用 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 生成 [!INCLUDE[wf2](../includes/wf2-md.md)] 应用程序时，可像在 Visual Studio 中那样，在 C# 和Visual Basic 代码中设置断点。 正如所料，工作流执行将在设置的每个断点处停止。

 断点具有三种状态： "*挂起*"、"*绑定*" 和 "*错误*"。 当您设置断点时，断点处于“挂起”状态，并且由一个空心的红色图标表示。 当运行时加载了工作流类型后，断点将变为“绑定”状态，并且由一个实心的红色图标表示。 如果为断点指定了不正确的格式，如同无效活动名称的情况一样，将出现一个错误窗口。 断点仍然会添加到断点窗口，但标有一个小“x”。

 可通过以下方式在工作流设计图面上设置活动断点：

- 右键单击该活动，然后选择 "断点" "**插入断点**"。

- 选择活动并按 F9。

- 从 "**调试**" 菜单中选择 "**新建断点**"。

     您也可以使用此选项在调试时设置新断点，这时调试器将在断点处停止。

    > [!NOTE]
    > 不支持在调用的工作流上设置断点。

### <a name="to-set-a-breakpoint-using-the-new-breakpoint-option-on-the-debug-menu"></a>使用“调试”菜单上的“新建断点”选项设置断点

1. 在 "**调试**" 菜单上，选择 "**新建断点**"。

2. 单击 "**在函数处中断**"。

     此时将打开 "**新建断点**" 对话框。

3. 使用以下语法在 "**函数**" 文本框中指定活动的名称： `QualifiedActivityId[:[FullClassName][:InstanceId]]`。

    > [!NOTE]
    > 或者，您可以通过指定工作流活动的绝对路径来设置断点，而不是使用 "**函数**" 文本框中的活动名称。 例如，假设你有一个名为**workflowconsoleapplication1.workflow1**的工作流解决方案和一个名为**workflow1.xaml**的解决方案，该解决方案使用名为**Delay1**的活动。 您可以使用活动名称**Delay1**或将路径指定为**Delay1： workflowconsoleapplication1.workflow1： workflow1.xaml**或 Delay1： workflowconsoleapplication1.workflow1 **： {workflow1.xaml}** 。

4. 选中 "**使用 IntelliSense** " 复选框以验证函数名称。

     如果未选中此复选框，则不会执行断点名称验证。

5. 从 "**语言**" 列表中选择 "**工作流**"。

6. 单击“确定”。

## <a name="see-also"></a>请参阅
 [调试](../workflow-designer/debugging-legacy-workflows.md)[用于 Windows Workflow Foundation 的 Visual Studio 调试程序的旧工作流（旧版）](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)