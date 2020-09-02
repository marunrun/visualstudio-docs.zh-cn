---
title: 开发工作流设计器的应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- DefaultWorkflowDesigner
- DefaultWorkflowDesigner.UI
helpviewer_keywords:
- Visual Studio 2010 Workflow Designer [WFD], overview
- Workflow Designer [WFD]
- Visual Studio 2010 Workflow Designer [WFD]
- Workflow Designer [WFD], overview
ms.assetid: 4cd062b1-b496-4668-bbc1-ee85545e066d
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 848300c54800e229ee1f487fc415bad45d982a6c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656829"
---
# <a name="developing-applications-with-the-workflow-designer"></a>使用工作流设计器开发应用程序
[!INCLUDE[wfd1](../includes/wfd1-md.md)] 是可视化设计器和调试器，用于以图形化的方式构造和调试 [!INCLUDE[wf](../includes/wf-md.md)] 开发环境中承载的 [!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)]中的 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 应用程序。 它可用于通过使用模板和活动设计器来撰写复合工作流应用程序、活动库或 [!INCLUDE[indigo1](../includes/indigo1-md.md)] 服务。 [!INCLUDE[crabout](../includes/crabout-md.md)] 工作流，请参阅 [.NET Framework 4&#93;的 Windows Workflow Foundation &#91; ](https://msdn.microsoft.com/library/9a23ea6b-d600-483e-89cd-8889cfec5f66)。

 下面是一些 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 的旧版本中没有，而在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 的新版本中增加的新设计功能：

- [!INCLUDE[wfd2](../includes/wfd2-md.md)] 是使用 [!INCLUDE[avalon1](../includes/avalon1-md.md)] 生成的。 这将改善活动设计器体验并提高大型和复杂工作流的性能。

- 现在可通过 [!INCLUDE[avalon2](../includes/avalon2-md.md)] 来设计自定义活动，并且使用 XAML 和编程模型来创建活动设计器也得到了简化。

- 实现了一个 Flowchart 活动，因此可以使用熟悉的流程图建模样式使程序流直观显示。

- [!INCLUDE[wfd2](../includes/wfd2-md.md)] 有一个新的变量设计器，可用于在工作流中声明变量和指定变量的作用域，从而将这些变量绑定到活动。

- 在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中，创作 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 工作流中的 Visual Basic 表达式时，[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 可提供完整的 IntelliSense 功能。

- 调试体验现在已延伸至 XAML，使您能在 XAML 工作流定义中设置断点并在运行时单步执行 XAML 代码，这提供类似于托管代码中的体验。

- 与以前的版本相比，在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 之外重新承载 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 得到了极大的简化，现在只需要几行代码。

- 新 <xref:System.Activities.Statements.Flowchart> 活动和其 [流程图](../workflow-designer/flowchart-activity-designer.md) 允许使用熟悉的流程图建模样式来可视化程序流。

- 消息传递活动得到了增强，可以编写完全声明性（无代码）的 [!INCLUDE[indigo1](../includes/indigo1-md.md)] 服务。

- **添加服务引用 ...** 使用功能可以自动生成用于访问 Web 服务的活动。

## <a name="in-this-section"></a>本节内容
 [使用工作流设计器](../workflow-designer/using-the-workflow-designer.md) 演示如何使用内置设计器创建新的活动和工作流项目，以及如何使用设计器提供的其他工具来处理参数、变量、表达式、导入和痕迹导航。

 [使用活动设计器](../workflow-designer/using-the-activity-designers.md) 描述系统提供的活动和模板及其设计器的类别。

 [用工作流设计器调试工作流](../workflow-designer/debugging-workflows-with-the-workflow-designer.md) 介绍如何执行传统调试过程以及如何调试 XAML 和表达式。

 [工作流设计器 UI 帮助](../workflow-designer/workflow-designer-ui-help.md) 包含由提供的对话框的上下文相关帮助主题 [!INCLUDE[wfd1](../includes/wfd1-md.md)] ，以及有关设计器 shell 功能、键盘快捷方式和错误消息的指导。

 [开发面向 .net 3.0 或 .net 3.5 Framework 的工作流应用程序](../workflow-designer/developing-workflow-applications-targeting-the-dotnet-3-0-or-dotnet-3-5-framework.md) 包含有关使用面向或的旧设计器的指南 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 。

 [设计器重新承载 &#91;WF 示例&#93;](https://msdn.microsoft.com/library/b676ad31-5f64-4d84-9a36-b4d7113a2f4d) 此示例演示如何创建用于包含设计器的 WPF 布局。

 [自定义活动设计器](https://msdn.microsoft.com/library/dcf14dca-ce6d-4278-96ba-062f0a679075) 本部分包含使用自定义设计器在工作流设计器中显示的活动示例。