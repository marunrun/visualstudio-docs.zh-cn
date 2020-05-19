---
title: 检查异常 - Visual Studio | Microsoft Docs
ms.date: 1/18/2020
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- exception helper, debugger, exception
- debugging [Visual Studio], exception helper, Examine an exception
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2dae1609486ec4f3462be89b0526467dd7414647
ms.sourcegitcommit: 8cbced0fb46959a3a2494852df1e41db1177a26c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76829755"
---
# <a name="inspect-an-exception-using-the-exception-helper"></a>使用异常帮助程序检查异常 

无论你的技术或专业水平如何，处理异常都是常见问题。 弄清楚为什么异常会导致代码中的问题可能是让人沮丧的经历。 当你在 Visual Studio 中调试异常时，我们希望通过为你提供相关的异常信息来帮助你更快地调试问题，从而减轻这种挫败感。

![异常帮助程序](media/debugger-exception-helper-default.png)

## <a name="pause-on-the-exception"></a>出现异常时暂停
当调试器因异常而中断时，该代码行的右侧会出现一个异常错误图标。 非模式异常帮助程序将在异常图标附近显示。

![代码行旁边的异常帮助程序](media/debugger-exception-helper-locerror.png)

## <a name="inspect-exception-info"></a>检查异常信息
你可以立即在异常帮助程序中读取异常类型和异常消息，以及异常是已引发还是未处理。 你可以通过单击“查看详细信息”链接来检查和查看异常对象的属性。

## <a name="analyze-null-references"></a>分析空引用
从 Visual Studio 2017 开始，对于 .Net 和 C/C++ 代码，当你命中 `NullReferenceException` 或 `AccessViolation` 时，你将在异常帮助程序中看到空分析信息。 分析显示为异常消息下方的文本。 在下图中，信息显示为“s 为空”。

![异常帮助程序空分析](media/debugger-exception-helper-default.png)


> [!NOTE]
> 托管代码中的空引用分析需要 .NET 版本 4.6.2。 通用 Windows 平台 (UWP) 和任何其他 .NET Core 应用程序当前均不支持空分析。 它仅在调试没有任何实时 (JIT) 代码优化的代码时可用。

## <a name="configure-exception-settings"></a>配置异常设置 
你可以在异常帮助程序的“异常设置”部分将调试器配置为在引发当前类型的异常时中断。 如果调试器在引发的异常处暂停，则可以使用复选框禁止在将来引发该异常类型时中断。 如果你不想在此特定异常在特定模块中引发时中断，请在“异常设置”窗口中的“例外引发位置:”下方勾选模块名称旁的复选框。 

## <a name="inspect-inner-exceptions"></a>检查内部异常 
如果异常具有任何内部异常 ([InnerException](https://docs.microsoft.com/dotnet/api/system.exception.innerexception))，则可以在异常帮助程序中查看它们。 如果存在多个异常，则可以使用调用堆栈上方显示的左右箭头在它们之间进行导航。

![具有内部异常的异常帮助程序](media/debugger-exception-helper-innerexception.png)

## <a name="inspect-rethrown-exceptions"></a>检查重新引发的异常
在异常 `thrown` 的情况下，异常帮助程序会显示引发第一次异常的调用堆栈。 如果多次引发该异常，则仅显示引发原始异常的调用堆栈。

![具有重新引发的异常的异常帮助程序](media/debugger-exception-helper-innerexception.png)

## <a name="share-a-debug-session-with-live-share"></a>与 Live Share 共享调试会话
在异常帮助程序中，你可以使用“启动 Live Share 会话...”链接来启动 [Live Share](https://docs.microsoft.com/visualstudio/liveshare/) 会话。加入 Live Share 会话的所有人都可以看到异常帮助程序以及任何其他调试信息。
