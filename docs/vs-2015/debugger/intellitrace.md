---
title: IntelliTrace | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.overview
helpviewer_keywords:
- debugger, recording execution history
- debugging, recording execution history
- IntelliTrace [Visual Studio ALM]
- IntelliTrace, debugging applications
- debugger, (See also IntelliTrace [Visual Studio ALM])
- debugging, (See also IntelliTrace [Visual Studio ALM])
- IntelliTrace, collecting data from Test Manager
- IntelliTrace
- Test Manager, debugging with IntelliTrace
- IntelliTrace, debugging after a crash
ms.assetid: 486bfec2-39bd-4d78-892a-42352128ee52
caps.latest.revision: 142
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a3a3e68874bb3295f6696bbdadb3c470a7f2a4ad
ms.sourcegitcommit: da5ebc29544fdbdf625ab4922c9777faf2bcae4a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2020
ms.locfileid: "82586620"
---
# <a name="intellitrace"></a>IntelliTrace
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本可在[IntelliTrace](/visualstudio/debugger/intellitrace)中找到。  
  
使用 IntelliTrace 记录和跟踪代码的执行历史记录时，可缩短调试应用程序所用的时间。 你可以更轻松地发现 Bug，因为 IntelliTrace 让你能够：  
  
- 记录特定事件  
  
   检查相关代码、调试程序事件期间“局部变量”**** 窗口中显示的数据以及函数调用信息  
  
- 调试难以重现或在部署中出现的错误  
  
  可以在 Visual Studio Enterprise 版（但不可在 Professional 或 Community 版）中使用 IntelliTrace。  
  
## <a name="what-do-you-want-to-do"></a>您希望做什么？  
  
|||  
|-|-|  
|**使用 IntelliTrace 调试应用程序：**<br /><br /> -显示过去的事件。<br />-显示对过去事件的调用信息。<br />-保存我的 IntelliTrace 会话。<br />-控制 IntelliTrace 收集的数据。|-   [演练：使用 IntelliTrace](../debugger/walkthrough-using-intellitrace.md)<br />     [IntelliTrace 功能](../debugger/intellitrace-features.md)<br />-   [配置 IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)<br />-   [历史调试](../debugger/historical-debugging.md)|  
|**在测试管理器中，在测试会话期间收集 IntelliTrace 数据**|-   [在手动测试中收集更多诊断数据](https://msdn.microsoft.com/library/bb5a2cc0-84f5-4dfe-9560-ca3d313aefd2)|  
|**从已部署的应用程序中收集 IntelliTrace 数据**|-   [使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)|  
|**从 IntelliTrace 日志文件（.iTrace 文件）中开始调试。**|-   [使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)|  
  
## <a name="what-apps-can-i-debug-with-intellitrace"></a><a name="IntelliTraceSupport"></a>哪些应用程序可以使用 IntelliTrace 进行调试？  
  
|||  
|-|-|  
|**支持**|-Visual Basic 和使用 .NET Framework 2.0 或更高版本的 Visual c # 应用程序。<br />     你可以调试大多数应用程序，包括 ASP.NET、Microsoft Azure、Windows 窗体、WCF、WPF、Windows 工作流、SharePoint 2010、SharePoint 2013 和 64 位应用。<br />     若要使用 IntelliTrace 调试 SharePoint 应用程序，请参阅[演练：使用 Intellitrace 调试 Sharepoint 应用程序](https://msdn.microsoft.com/library/4bd80d2f-f680-4bf4-81c3-f14e8185f6a4)。<br />     若要使用 IntelliTrace 调试 Microsoft Azure 的应用，请参阅[使用 intellitrace 和 Visual Studio 调试已发布的云服务](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md)。|  
|**有限支持**|-基于实验性的 F # 应用<br />-仅支持适用于事件的 Windows 应用商店应用|  
|**不支持**|-C + +、其他语言和脚本<br />-Windows 服务、Silverlight、Xbox 或[!INCLUDE[winmobile](../includes/winmobile-md.md)]应用|  
  
> [!NOTE]
> 如果要调试已经在运行的进程，则不能使用 IntelliTrace。 进程开始时，你必须启动 IntelliTrace。  
  
## <a name="why-debug-with-intellitrace"></a><a name="IntelliTraceVSTraditional"></a>为何使用 IntelliTrace 进行调试？  
 传统或实时** 调试仅显示应用程序的当前状态以及有关过去事件的有限数据。 要么必须根据应用程序的当前状态推断这些事件，要么必须通过重新运行应用程序以重新生成这些事件。  
  
 IntelliTrace 通过记录特定事件和这些时间点的数据，扩展此传统调试体验。 这让你能够不重启应用程序即可查看应用程序中发生了什么，特别是在单步执行到 Bug 处时。 IntelliTrace 在传统调试期间会默认启用，并以不可见的方式自动收集数据。 这样，你即可轻松地在传统调试和 IntelliTrace 调试之间进行切换来查看该记录信息。 请参阅 intellitrace[功能](../debugger/intellitrace-features.md)和[intellitrace 收集哪些数据？](#WhatData)  
  
 IntelliTrace 还可帮助你调试难以重现或在部署时出现的错误。 可以收集 IntelliTrace 数据并将其保存为 IntelliTrace 日志文件（.iTrace 文件）。 .iTrace 文件包含有关异常、性能事件、Web 请求、测试数据、线程、模块和其他系统信息的详细信息。 可以在 Visual Studio Enterprise 中打开此文件、选择一个项，然后使用 IntelliTrace 开始调试。 这让你能够转到文件中的任何事件并查看该时间点上有关应用程序的特定详细信息。  
  
 你可以从这些源中保存 IntelliTrace 数据：  
  
- Visual Studio 2015 企业版或早期版本的 Visual Studio Ultimate 中的 IntelliTrace 会话。  
  
- Microsoft 测试管理器中的测试会话  
  
- IIS 上托管的 ASP.NET Web 应用程序，或使用 Microsoft Monitoring Agent（单独使用或与 System Center 2012 一起使用）时在部署中运行的 SharePoint 2010 和 SharePoint 2013 应用程序。 请参阅[使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)并使用[Microsoft Monitoring Agent 进行监视](https://technet.microsoft.com/library/dn465153.aspx)。  
  
  下面是一些示例，说明 IntelliTrace 如何帮助你进行调试：  
  
- 你的应用程序损坏了一个数据文件，但是你不知道此事件的发生位置。  
  
   如果不使用 IntelliTrace，则必须浏览代码以查找所有可能的文件访问，在这些访问上放置断点，并重新运行应用程序以查找出现问题的位置。 如果使用 IntelliTrace，则在每个事件发生时，可以查看收集的所有文件访问事件和有关应用程序的特定详细信息。  
  
- 发生异常。  
  
   如果不使用 IntelliTrace，你会获得有关异常的消息，但不会获得有关导致异常的事件的大量信息。 你可以检查调用堆栈，以查看导致异常的调用链，但不能查看这些调用过程中发生的事件序列。 如果使用 IntelliTrace，你可以检查在异常之前发生的事件。  
  
- 你的应用程序在测试计算机上崩溃，但在开发计算机上成功运行。  
  
   可以从 Microsoft 测试管理器中收集 IntelliTrace 数据，将该数据保存到 .iTrace 文件，并将此文件附加到 Team Foundation Server 工作项以备以后调查使用。 请参阅[在手动测试中收集更多诊断数据](https://msdn.microsoft.com/library/bb5a2cc0-84f5-4dfe-9560-ca3d313aefd2)和[使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)。  
  
- 在已部署的应用程序中发生 Bug 或崩溃。  
  
   对于基于 Microsoft Azure 的应用，在发布应用程序之前，可以配置 IntelliTrace 数据收集。 应用程序运行时，IntelliTrace 会将数据保存到 .iTrace 文件。 请参阅[使用 IntelliTrace 和 Visual Studio 调试已发布的云服务](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md)。  
  
   对于 IIS 7.0、7.5 和 8.0 上托管的 ASP.NET Web 应用程序，以及 SharePoint 2010 或 SharePoint 2013 应用程序，请使用 Microsoft Monitoring Agent（单独使用或与 System Center 2012 一起使用），以备将 IntelliTrace 数据保存到 .iTrace 文件中。  
  
   当你需要诊断部署中的应用程序的问题时，这会很有用。 请参阅[使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)。  
  
## <a name="what-data-does-intellitrace-collect"></a><a name="WhatData"></a>IntelliTrace 收集哪些数据？  
 **收集事件信息**  
  
 默认情况下，IntelliTrace 仅记录 IntelliTrace 事件：调试程序事件、异常、.NET Framework 事件以及可帮助进行调试的其他系统事件。 你可以选择想要收集的 IntelliTrace 事件的类型（始终收集的调试器事件和异常除外）。 请参阅[配置 IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)。  
  
- **调试器事件**  
  
   IntelliTrace 始终记录 Visual Studio 调试器中发生的事件。 例如，启动应用程序是一个调试程序事件。 其他调试程序事件包括会导致应用程序中断执行的停止事件。 例如，你的程序命中断点、命中跟踪点或执行“步骤”**** 命令。  
  
   为了帮助提高性能，IntelliTrace 不记录调试器事件的每个可能的值， 而是记录以下值：  
  
  - “局部变量”**** 窗口中的值。 请将“局部变量”**** 窗口保持打开状态以查看这些值。  
  
  - “自动”**** 窗口中的值（仅当“自动”**** 窗口处于打开状态时）  
  
  - 在将鼠标指针移到源窗口中的变量的上方以查看其值时显示的数据提示中的值。 IntelliTrace 不收集固定数据提示中的值。  
  
- **异常**  
  
   IntelliTrace 会记录异常类型和以下各类异常的消息：  
  
  - 已处理的异常（已引发并捕获异常）  
  
  - 未经处理的异常  
  
- **.NET Framework 事件**  
  
   默认情况下，IntelliTrace 记录最常见的 .NET Framework 事件。 例如：  
  
  - 对于“文件访问”事件，IntelliTrace 将收集文件名。  
  
  - 对于选中复选框事件，IntelliTrace 将收集复选框状态和文本。  
  
- **SharePoint 2010 和 SharePoint 2013 应用程序事件**  
  
   你可以为在 Visual Studio 外运行的 SharePoint 2010 和 2013 应用程序记录用户配置文件事件以及一部分统一日志记录系统 (ULS) 事件。 你可以将这些事件保存到 .iTrace 文件中。 需要 Visual Studio Enterprise 2015、以前版本的 Visual Studio Ultimate 或[Microsoft Monitoring Agent](https://go.microsoft.com/fwlink/?LinkID=309771)在**跟踪**模式下运行。  
  
   打开 .iTrace 文件时，输入 SharePoint 相关 ID 以查找其匹配的 Web 请求，查看记录事件，并从特定事件开始调试。 如果文件包含未经处理的异常，可以选择相关 ID，开始调试异常。  
  
   请参阅：  
  
  - [使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)  
  
  - [使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)  
  
  - [演练：使用 IntelliTrace 调试 SharePoint 应用程序](https://msdn.microsoft.com/library/4bd80d2f-f680-4bf4-81c3-f14e8185f6a4)  
  
  **收集函数调用信息**  
  
  可以配置 IntelliTrace 以收集函数的调用信息。 此信息使你可以查看调用堆栈历史记录，并能在代码中向后移动和向前移动调用。 对于每个函数调用，IntelliTrace 将记录此数据：  
  
- 函数名称  
  
- 在函数入口点作为参数传递并在函数退出点返回的基元数据类型的值  
  
- 读取或更改自动属性时该属性的值  
  
- 指向第一级子对象的指针，而不是它们的值，除非它们为 null  
  
> [!NOTE]
> IntelliTrace 仅收集数组中的头 256 个对象和字符串的头 256 个字符。  
  
 请参阅[配置 IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)。  
  
 **收集模块信息**  
  
 若要控制 IntelliTrace 收集的调用信息量，请仅指定你关注的模块。 这有助于在收集期间提高应用程序的性能。 请参阅[配置 IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)。  
  
## <a name="will-intellitrace-slow-down-my-application"></a><a name="AffectPerformance"></a>IntelliTrace 会让我的应用程序速度变慢吗？  
 默认情况下，IntelliTrace 仅收集所选 IntelliTrace 事件的数据。 这可能会让应用程序的速度变慢，也可能不会，具体取决于代码的结构和组织。 例如，如果 IntelliTrace 经常记录某个事件，则这可能会让应用程序的速度变慢。 它还可能会让你考虑重构应用程序。  
  
 收集调用信息可能会让应用程序的速度显著变慢。 它还可能增加你保存到磁盘上的 IntelliTrace 日志文件（.iTrace 文件）的大小。 若要尽可能减少这些影响，请仅收集你关注的模块的调用信息。  若要更改 .iTrace 文件的最大大小，请转到“工具”****、“选项”****、IntelliTrace****、“高级”****。 请参阅[配置 IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)。  
  
## <a name="in-this-section"></a>在本节中  
 [IntelliTrace 功能](../debugger/intellitrace-features.md)  
  
 [配置 IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)  
  
 [在难以重现的 Bug 中包含诊断跟踪数据](https://msdn.microsoft.com/library/944ae9af-5a55-4c58-b520-0108c03b3564)  
  
 [诊断部署后出现的问题](../debugger/diagnose-problems-after-deployment.md)  
  
 [使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)  
  
### <a name="blogs"></a>博客  
 [Visual Studio ALM + Team Foundation Server](https://devblogs.microsoft.com/devops/welcome-to-the-visual-studio-alm-team-foundation-server-blog/)  
  
### <a name="forums"></a>论坛  
 [Visual Studio 诊断](https://social.msdn.microsoft.com/Forums/vsdebug)
