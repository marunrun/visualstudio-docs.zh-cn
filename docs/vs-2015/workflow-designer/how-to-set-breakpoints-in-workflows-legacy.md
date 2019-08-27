---
title: 如何：在工作流 （旧版） 中设置断点 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7cec06813890523e604234ccefdbcd7d1de31653
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444180"
---
# <a name="how-to-set-breakpoints-in-workflows-legacy"></a>如何：在工作流中设置断点（旧版）
本主题介绍如何在使用旧 [!INCLUDE[wf](../includes/wf-md.md)] 生成的 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 应用程序中设置断点。 在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 应用程序需要面向 [!INCLUDE[wf2](../includes/wf2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。  
  
 当使用 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中的旧 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 生成 [!INCLUDE[wf2](../includes/wf2-md.md)] 应用程序时，可像在 Visual Studio 中那样，在 C# 和Visual Basic 代码中设置断点。 正如所料，工作流执行将在设置的每个断点处停止。  
  
 断点具有三种状态：*挂起*，*绑定*，和*错误*。 当您设置断点时，断点处于“挂起”状态，并且由一个空心的红色图标表示。 当运行时加载了工作流类型后，断点将变为“绑定”状态，并且由一个实心的红色图标表示。 如果为断点指定了不正确的格式，如同无效活动名称的情况一样，将出现一个错误窗口。 断点仍然会添加到断点窗口，但标有一个小“x”。  
  
 可通过以下方式在工作流设计图面上设置活动断点：  
  
- 右键单击该活动，然后选择**断点 \ 插入断点**。  
  
- 选择活动并按 F9。  
  
- 选择**新断点**从**调试**菜单。  
  
     您也可以使用此选项在调试时设置新断点，这时调试器将在断点处停止。  
  
    > [!NOTE]
    > 不支持在调用的工作流上设置断点。  
  
### <a name="to-set-a-breakpoint-using-the-new-breakpoint-option-on-the-debug-menu"></a>使用“调试”菜单上的“新建断点”选项设置断点  
  
1. 上**调试**菜单中，选择**新断点**。  
  
2. 单击**在函数处中断**。  
  
     **新断点**对话框随即打开。  
  
3. 指定的名称中的活动**函数**文本框中，使用以下语法： `QualifiedActivityId[:[FullClassName][:InstanceId]]`。  
  
    > [!NOTE]
    > （可选） 而不是使用中的活动名称**函数**文本框中，您可以通过指定的工作流活动的绝对路径来设置断点。 例如，假设有一个名为工作流解决方案**WorkflowConsoleApplication1**和名为解决方案中的工作流**Workflow1** ，它使用一个名为活动**Delay1**. 可以使用活动名称**Delay1**或将路径指定为**Delay1:WorkflowConsoleApplication1.Workflow1**或**Delay1:WorkflowConsoleApplication1.Workflow1: {6614886A-608E-412B-BF98-99FF1559DDDF}**。  
  
4. 选择**使用 IntelliSense**复选框，以验证函数名称。  
  
     如果未选中此复选框，则不会执行断点名称验证。  
  
5. 选择**工作流**从**语言**列表。  
  
6. 单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [调试旧版工作流](../workflow-designer/debugging-legacy-workflows.md)   
 [调用 Visual Studio Debugger for Windows Workflow Foundation（旧版）](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)