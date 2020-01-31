---
title: 检查异常-Visual Studio |Microsoft Docs
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76829755"
---
# <a name="inspect-an-exception-using-the-exception-helper"></a>使用异常帮助器检查异常 

处理异常是一个常见问题，不管你的技术或专业水平。 这可能是一种令人沮丧的体验，它可以判断异常为何会导致代码中出现问题。 在 Visual Studio 中调试异常时，我们想要通过提供相关的异常信息来帮助你更快地调试问题，从而减少这项不满。

![异常帮助器](media/debugger-exception-helper-default.png)

## <a name="pause-on-the-exception"></a>异常时暂停
当调试器在异常上中断时，该代码行的右侧会出现异常错误图标。 非模式异常帮助器将出现在异常图标附近。

![代码行旁边的异常帮助器](media/debugger-exception-helper-locerror.png)

## <a name="inspect-exception-info"></a>检查异常信息
你可以立即在异常帮助程序中读取异常类型和异常消息，以及是否引发了异常或未处理的异常消息。 可以通过单击 "**查看详细信息**" 链接来检查和查看异常对象的属性。

## <a name="analyze-null-references"></a>分析空引用
从 Visual Studio 2017 开始，适用于 .Net 和 C/C++ code，当你命中 `NullReferenceException` 或 `AccessViolation`时，你会在异常帮助程序中看到 null 分析信息。 分析显示为异常消息下的文本。 在下图中，信息显示为 "**s**为 null"。

![异常帮助程序 null 分析](media/debugger-exception-helper-default.png)


> [!NOTE]
> 托管代码中的空引用分析需要 .NET 版本4.6.2。 通用 Windows 平台（UWP）和任何其他 .NET Core 应用程序当前不支持 Null 分析。 仅当调试的代码不具有任何实时（JIT）代码优化时，它才可用。

## <a name="configure-exception-settings"></a>配置异常设置 
您可以将调试器配置为在异常帮助器的 "**异常设置**" 部分引发当前类型的异常时中断。 如果调试器在引发的异常处暂停，则可以使用此复选框禁用在将来引发的异常类型的中断。 如果你不希望在此特定模块中引发时中断此特定异常，则在 "**异常设置**" 窗口中的 "**从以下项中引发时**" 下的模块名称之前勾选该复选框。 

## <a name="inspect-inner-exceptions"></a>检查内部异常 
如果异常包含任何内部异常（[InnerException](https://docs.microsoft.com/dotnet/api/system.exception.innerexception)，你可以在异常帮助器中查看它们。 如果存在多个异常，则可以使用调用堆栈上方显示的向左箭头和向右箭头在它们之间导航。

![包含内部异常的异常帮助器](media/debugger-exception-helper-innerexception.png)

## <a name="inspect-rethrown-exceptions"></a>检查再次引发的异常
在异常已 `thrown` 的情况下，异常帮助器显示第一次引发异常时的调用堆栈。 如果多次引发异常，则只显示来自原始异常的调用堆栈。

![引发异常的异常帮助器](media/debugger-exception-helper-innerexception.png)

## <a name="share-a-debug-session-with-live-share"></a>与 Live Share 共享调试会话
在异常帮助程序中，可以使用 "**启动 Live Share 会话**" 链接启动[Live Share](https://docs.microsoft.com/visualstudio/liveshare/)会话 .。。加入 Live Share 会话的任何人都可以查看异常帮助程序以及任何其他调试信息。
