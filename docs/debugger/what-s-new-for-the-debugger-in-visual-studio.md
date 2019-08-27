---
title: 什么是 Visual Studio 2017 中调试器的新增功能 |Microsoft Docs
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
ms.openlocfilehash: 9c6f2eb4be56be8cf5e25c3238a91819df3bc574
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901368"
---
# <a name="whats-new-for-the-debugger-in-visual-studio-2017"></a>Visual Studio 2017 中调试器的新变化

调试器包括这些新功能：

- 版本 15.5 中中的新增功能**快照调试器**感兴趣的代码执行时，获取在生产中的应用的快照。 若要指示该调试器拍摄快照，可以在代码中设置快照点和记录点。 通过该调试器，可精确查看出错的内容，而不会影响生产应用程序的流量。 快照调试程序有助于大幅减少用于解决生产环境中发生的问题的时间。

    快照集合适用于在 Azure App Service 中运行的以下 Web 应用：

  * 在 .NET Framework 4.6.1 或更高版本上运行的 ASP.NET 应用程序。
  * 在 Windows 中的 .Net Core 2.0 或更高版本上运行的 ASP.NET Core 应用程序。

    有关详细信息，请参阅[使用 Snapshot Debugger 调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)。

- 仅限 15.5 Visual Studio Enterprise 中中的新增功能**IntelliTrace 后退**单步执行事件也会自动编制每个断点和调试程序应用程序的快照。 凭借记录的快照便可以返回到上一个断点或步骤，并查看当时应用程序的状态。 如果希望查看以前的应用程序状态，但不想重新启动调试或重新创建所需应用状态，使用 IntelliTrace 后退可以节省时间。

    可以通过使用调试工具栏中的“后退”和前进”按钮浏览和查看快照。 这些按钮用于浏览“诊断工具”窗口中“事件”选项卡上显示的事件。

    ![“后退”和“前进”按钮](../debugger/media/intellitrace-step-back-icons-description.png  "Step Backward and Forward buttons")

    有关详细信息，请参阅[使用 IntelliTrace 检查上一应用状态](../debugger/view-historical-application-state.md)页。

- **异常帮助器**替换异常助手，将出现在错误发生位置的非模式对话框。 **异常帮助程序**提供更快地访问任何内部异常，调试器使用 （如果可用），其他分析和立即访问**异常设置**异常。 异常帮助器还可以拖动到浮点视图，如果它阻止您需要查看的内容。

    例如， **NullReferenceException**现在将显示具有空引用 （额外信息） 的变量。

    ![调试器的异常帮助器](../debugger/media/dbg-exception-helper.png "DbgExceptionHelper")

    有关详细信息，请参阅 [Using the New Exception Helper in Visual Studio](https://blogs.msdn.microsoft.com/visualstudioalm/2016/03/31/using-the-new-exception-helper-in-visual-studio-15-preview/)（使用 Visual Studio 中的新异常帮助器）博客文章。

- 现在可以运行的代码在调试器中暂停时通过选择行**执行运行到此处**绿色箭头图标 （你将看到一行代码将鼠标悬停时图标）。 这消除了需要设置临时断点。

    ![调试器的运行时单击](../debugger/media/dbg-run-to-click.png "DbgRunToClick")

- 你可以设置条件中发生异常**异常设置**对话框 (可以执行此操作通过使用**编辑条件**异常设置对话框中或通过右键单击菜单上的图标异常。）当前支持的条件包括模块名称要包括或排除异常。

    ![在出现异常的条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

- 附加到进程对话框的包含一个新的搜索功能，可帮助你更快速确定需要附加到进程。

    ![中的搜索将附加到进程](../debugger/media/dbg-attach-to-process-search.png "DbgAttachToProcessSearch")

有关这些新功能的详细信息，请参阅[发行说明[!include[vs_dev15](../misc/includes/vs_dev15_md.md)] ](/visualstudio/releasenotes/vs2017-relnotes)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.md)
- [初探调试器](../debugger/debugger-feature-tour.md)