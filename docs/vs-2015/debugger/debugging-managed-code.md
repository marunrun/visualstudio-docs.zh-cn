---
title: 调试托管的代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging managed code
- debugging ASP.NET Web applications, managed code
- managed code, debugging
ms.assetid: fa3aff01-c271-4aa7-b5b1-def560471c84
caps.latest.revision: 37
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 39076459f684aafce4e800ecad6341d120aac480
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691449"
---
# <a name="debugging-managed-code"></a>调试托管代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本节包含了托管应用程序或使用面向公共语言运行时的语言（如 Visual Basic、C# 和 C++）编写的应用程序的常见调试问题和调试技术。 此处介绍的技术都是高级技术。 有关详细信息，请参阅[使用调试器](../debugger/debugger-basics.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [“输出”窗口中的诊断消息](../debugger/diagnostic-messages-in-the-output-window.md)  
 描述 <xref:System.Diagnostics.Debug> 和 <xref:System.Diagnostics.Trace> 类，通过这些类，您可以向“输出”窗口写入运行时消息。 这些类中包含的输出方法支持两种信息输出：不中断执行的信息输出以及在指定条件失败时也会中断执行的信息输出。  
  
 [托管代码中的断言](../debugger/assertions-in-managed-code.md)  
 描述托管代码中的断言，该断言用于测试作为 `Assert` 方法的自变量指定的条件。 此外，本主题还提供代码示例、有关使用 <xref:System.Diagnostics.Debug> 和 <xref:System.Diagnostics.Trace> 类方法的信息、代码调试版和发布版中的注意事项、副作用、断言参数、自定义断言行为和配置文件。  
  
 [Visual Basic 中的 Stop 语句](../debugger/stop-statements-in-visual-basic.md)  
 描述 `Stop` 语句，该语句提供了一种设置断点的替代方法。 还提供了代码示例并对 `Stop` 语句和 `End` 语句以及 `Stop` 和 `Assert` 语句进行了比较。  
  
 [演练：调试 Windows 窗体](../debugger/walkthrough-debugging-a-windows-form.md)  
 提供创建 Windows 窗体并调试该窗体的逐步骤说明。 Windows 窗体（托管 Windows 应用程序的标准组件）是最常见的托管应用程序之一。 本演练使用 Visual C# 和 Visual Basic，不过使用 C++ 创建 Windows 窗体的方法通常与此类似。  
  
 [调试 OnStart 方法](../debugger/how-to-debug-the-onstart-method.md)  
 提供使你能够调试托管 Windows 服务的 `OnStart` 方法的代码示例。 若要调试 Windows 服务的 `OnStart` 方法，您必须另外添加几行代码以模拟该服务。  
  
 [Mixed-Mode Debugging](../debugger/debugging-mixed-mode-applications.md)  
 讨论调试混合模式的应用程序。 这表示合并本机代码和托管代码的任何应用程序。  
  
 [错误：由于系统上启用了内核调试程序，因此不可能进行调试](../debugger/error-debugging-isn-t-possible-because-a-kernel-debugger-is-enabled-on-the-system.md)  
 描述当尝试在以调试模式启动的 [!INCLUDE[win7](../includes/win7-md.md)]、[!INCLUDE[wiprlhext](../includes/wiprlhext-md.md)]、[!INCLUDE[winxp](../includes/winxp-md.md)]、[!INCLUDE[Win2kFamily](../includes/win2kfamily-md.md)] 或 Windows NT 系统上调试托管代码时出现的错误消息。  
  
 [JIT 优化和调试](../debugger/jit-optimization-and-debugging.md)  
 描述调试时 JIT 优化的作用。  
  
 [调试 LINQ 和 DLINQ](../debugger/debugging-linq.md)  
 讨论用于调试 LINQ 查询的技术。  
  
 [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)  
 描述如何使用“并行任务” 和“并行堆栈”工具窗口调试并行应用程序。  
  
## <a name="related-sections"></a>相关章节  
 [IntelliTrace](../debugger/intellitrace.md)  
 通过使用 IntelliTrace 记录应用的执行历史记录来更快更轻松地发现 Bug。 通过记录的事件和调用向后移动和向前移动以在关键时间点检查您应用的状态。 调试代码，而无需设置很多断点或频繁重新启动应用。 需要 Visual Studio Ultimate。  
  
 [跟踪应用程序和在应用程序中插入检测点](https://msdn.microsoft.com/library/773b6fc4-9013-4322-b728-5dec7a72e743)  
 描述跟踪（一种用于监视运行中应用程序的执行情况的方法）和检测（将跟踪语句放在代码中的重要位置）。 此主题还提供了指向介绍以下内容的主题的链接：检测和跟踪、跟踪开关、跟踪侦听器、跟踪应用程序中的代码、将跟踪语句添加到应用程序代码，以及使用 <xref:System.Diagnostics.Debug> 和 <xref:System.Diagnostics.Trace> 进行有条件地编译。  
  
 [/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)  
 描述将 <xref:System.Diagnostics.DebuggableAttribute> 添加到用 C++ 编写的代码的链接器选项。 在使用调试功能（如使用 C++ 附加）时需要此特性。  
  
 [调试 Windows 服务应用程序](https://msdn.microsoft.com/library/63ab0800-0f05-4f1e-88e6-94c73fd920a2)  
 提供调试 Windows 服务应用程序的注意事项，其中包括：设置、附加到进程、调试服务的 `OnStart` 方法中的代码和 Main 方法中的代码、设置断点以及使用服务控制管理器启动、停止、暂停和继续服务。  
  
 [调试和分析](https://msdn.microsoft.com/library/4a04863e-2475-46f4-bc3f-3c11510c2a4b)  
 探讨如何调试 .NET Framework 应用程序和配置要求。  
  
 [调试脚本和 Web 应用程序](../debugger/debugging-web-applications-and-script.md)  
 描述在调试脚本和 Web 应用程序时可能会遇到的常见调试问题和技术。  
 此版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中新增的调试功能的说明。  
  
 [调试主页](../debugger/debugging-in-visual-studio.md)  
 提供指向调试文档的较大章节的链接。 涉及的信息包括：调试器的新增功能，设置和准备，断点，处理异常，编辑和继续，调试托管代码，调试 Visual C++ 项目，调试 COM 和 ActiveX，调试 DLL，调试 SQL，以及用户界面参考。  
  
## <a name="see-also"></a>请参阅  
 [演练：在设计时调试自定义 Windows 窗体的控件](https://msdn.microsoft.com/library/1fd83ccd-3798-42fc-85a3-6cba99467387)   
 [调试器安全](../debugger/debugger-security.md)   
 [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)
