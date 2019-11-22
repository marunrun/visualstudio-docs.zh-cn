---
title: Debug Store apps
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 48a85bcf-290b-4390-9993-f6f9dd73ad03
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2be61a066157b203e4d09ff5f5dff5340dc0ec67
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298341"
---
# <a name="debug-store-apps-in-visual-studio"></a>在 Visual Studio 中调试应用商店应用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以通过 Visual Studio 调试器控制程序的执行并检查其状态。 可以使用调试器查找 Windows 应用商店应用中出现缺陷的原因，还可以确切地了解应用的工作方式。 当在调试器中暂停（中断）执行时，Visual Studio 将显示源文件，该源文件包含执行代码并突出显示执行语句。 可以查看变量值、执行函数的调用堆栈以及程序状态的其他方面。 一次可使用一个语句来继续执行（分步完成）程序，以查看语句如何更改该程序的值。 在使用 JavaScript 编写的应用中，你可以检查并操作页面的 DOM。

## <a name="in-this-section"></a>本节内容

|||
|-|-|
|[启动调试会话 (JavaScript)](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md)|“如何启动调试会话”描述了用于针对 JavaScript 应用配置和启动调试会话的不同选项。|
|[在调试会话中控制执行 (JavaScript)](../debugger/control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript.md)|调试器导航将通过简单的应用来演示如何启动和停止调试、如何在代码中导航以及如何查看程序状态。|
|[快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)|调试 HTML 和 CSS 演示了如何使用实时 DOM 检查工具以交互方式调试 JavaScript 应用，以查看和修改 HTML 和 CSS。|
|[快速入门：调试 JavaScript](../debugger/quickstart-debug-javascript-using-the-console.md)|Debug JavaScript using the console shows you how to interactively debug a JavaScript app using [JavaScript Console commands](../debugger/javascript-console-commands.md).|
|[启动调试会话（VB、C#、C++ 和 XAML）](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)|“如何启动调试会话（Visual C++、Visual C# 和 Visual Basic）”描述了用于针对应用（使用 Visual C++、Visual C# 或 Visual Basic 编写而成）配置和启动调试会话的不同选项。|
|[导航调试会话（Xaml 和 C#）](../debugger/navigate-a-debugging-session-in-visual-studio-xaml-and-csharp.md)|调试器导航将通过简单的应用来演示如何启动和停止调试、如何在代码中导航以及如何查看和更改程序状态。|
|[触发 Windows 应用商店的挂起、继续和后台事件](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)|调试器将禁用挂起、继续和终止应用的 Windows 进程生命期管理 (PLM) 事件。 你可以从调试器工具栏触发这些事件。<br /><br /> 通过后台任务，可执行某些重要操作，即便应用已挂起也是如此。 调试器使你能够启动并调试这些后台任务。|

## <a name="see-also"></a>请参阅
 [Debugging in Visual Studio (in the MSDN Library)](https://go.microsoft.com/fwlink/?LinkID=226896)
