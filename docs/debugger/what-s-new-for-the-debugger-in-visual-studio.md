---
title: Visual Studio 2017 中调试器的新变化 | Microsoft Docs
titleSuffix: ''
ms.date: 01/22/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, what's new
- what's new [debugger]
- debugging [Visual Studio], what's new
- what's new [Visual Studio], debugging
ms.assetid: 2aed9caa-2384-4e49-8595-82d8b06cf271
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 523867a8f9aa074e9122c74deb8bcd91cddd8bee
ms.sourcegitcommit: 9a66f1c31cc9eba0b5231af72da1d18761a9c56a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2020
ms.locfileid: "75944216"
---
# <a name="whats-new-for-the-debugger-in-visual-studio-2017"></a>Visual Studio 2017 中调试器的新变化

调试器包括以下新功能：

- 版本 15.5 中的新增功能：当执行你感兴趣的代码时，Snapshot Debugger 会为生产中的应用拍摄快照。 若要指示该调试器拍摄快照，可以在代码中设置快照点和记录点。 通过该调试器，可精确查看出错的内容，而不会影响生产应用程序的流量。 快照调试程序有助于大幅减少用于解决生产环境中发生的问题的时间。

    快照集合适用于在 Azure App Service 中运行的以下 Web 应用：

  * 在 .NET Framework 4.6.1 或更高版本上运行的 ASP.NET 应用程序。
  * 在 Windows 中的 .Net Core 2.0 或更高版本上运行的 ASP.NET Core 应用程序。

    有关详细信息，请参阅[使用 Snapshot Debugger 调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)。

- 仅在 Visual Studio 企业版版本 15.5 中可用的新增功能：IntelliTrace 后退会在每个断点处及调试器步骤事件发生时自动拍摄应用程序的快照。 凭借记录的快照便可以返回到上一个断点或步骤，并查看当时应用程序的状态。 如果希望查看以前的应用程序状态，但不想重新启动调试或重新创建所需应用状态，使用 IntelliTrace 后退可以节省时间。

    可以通过使用调试工具栏中的“后退”和前进”按钮浏览和查看快照。  这些按钮用于浏览“诊断工具”窗口中“事件”选项卡上显示的事件。 

    ![“后退”和“前进”按钮](../debugger/media/intellitrace-step-back-icons-description.png  "“后退”和“前进”按钮")

    有关详细信息，请参阅[使用 IntelliTrace 检查上一应用状态](view-historical-application-state.md)页。

- 异常帮助程序会替换异常情况助手，并在发生错误的非模式对话框中显示。 异常帮助程序提供对任何内部异常的快速访问、调试器的其他分析（如果可用）以及对异常的“异常设置”的即时访问 。 如果异常帮助程序挡住了需要查看的内容，你也可以将其拖到浮动视图。

    例如，NullReferenceException 现在显示具有空引用的变量（额外信息）。

    ![调试器的异常帮助程序](../debugger/media/dbg-exception-helper.png "DbgExceptionHelper")

    有关详细信息，请参阅 [Using the New Exception Helper in Visual Studio](https://devblogs.microsoft.com/devops/using-the-new-exception-helper-in-visual-studio-15-preview/)（使用 Visual Studio 中的新异常帮助器）博客文章。

- 现在，你可以通过选择“将执行运行到此处”绿色箭头图标（光标悬停在代码行上时即可看到此图标），从而在调试器中暂停时运行到某一代码行。 这样就无需设置临时断点。

    ![调试器的“运行到单击处”](../debugger/media/dbg-run-to-click.png "DbgRunToClick")

- 你可以在“异常设置”对话框中设置异常条件（可以使用“异常设置”对话框中的“编辑条件”图标，或使用异常的右键单击菜单来执行此操作 。）当前支持的条件包括要包括在异常中或排除在异常外的模块名称。

    ![设置异常条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

- “附加到进程”对话框包含一项新的搜索功能，可帮助你更快速地识别需要附加到的进程。

    ![在“附加到进程”中搜索](../debugger/media/dbg-attach-to-process-search.png "DbgAttachToProcessSearch")

有关这些新功能的详细信息，请参阅 [[!include[vs_dev15](../misc/includes/vs_dev15_md.md)]](/visualstudio/releasenotes/vs2017-relnotes) 的发行说明。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)