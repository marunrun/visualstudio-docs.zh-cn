---
title: 将消息发送到“输出”窗口 | Microsoft Docs
ms.date: 11/08/2018
ms.topic: how-to
helpviewer_keywords:
- diagnostic messages [C#]
- System.Diagnostics.Debug class, Output window
- messages, diagnostic
- Debug.Print replacements
- diagnosis
- Output window, diagnostic messages
- System.Diagnostics.Trace class, Output window
- Trace class, diagnostic messages
- diagnostics
- debugger, Output window
- debugging [Visual Studio], diagnostic messages in Output window
- Debug class
ms.assetid: 386e9524-be17-4573-83fb-4f7c5cae0be0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 85d3c146775ac06b3118186738ee74932a4c452a
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350467"
---
# <a name="send-messages-to-the-output-window"></a>将消息发送到“输出”窗口

可以使用 <xref:System.Diagnostics.Debug> 类或 <xref:System.Diagnostics.Trace> 类将运行时消息发送到**输出**窗口中，这两个类是 <xref:System.Diagnostics> 类库的一部分。 如果只想在程序的*调试*版本中输出，使用 <xref:System.Diagnostics.Debug> 类。 如果想同时在*调试*和*发行*版本中输出，使用 <xref:System.Diagnostics.Trace> 类。

## <a name="output-methods"></a>输出方法
 <xref:System.Diagnostics.Trace> 和 <xref:System.Diagnostics.Debug> 类提供下列输出方法：

- 各种 `Write` 方法，在执行不中断的情况下输出信息。 这些方法取代了在 Visual Basic 早期版本中使用的 `Debug.Print` 方法。

- <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 和 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> 方法，如果指定的条件失败，这些方法将中断执行并输出信息。 默认情况下，`Assert` 方法显示对话框中的信息。 有关详细信息，请参阅[托管代码中的断言](../debugger/assertions-in-managed-code.md)。

- <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> 和 <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName> 方法，它们总是中断执行并输出信息。 默认情况下，在对话框中显示 `Fail` 方法信息。

**输出**窗口还可以显示下列信息：

- 调试器已经加载或卸载的模块。

- 引发的异常。

- 退出的进程。

- 退出的线程。

## <a name="see-also"></a>请参阅
- [调试器安全](../debugger/debugger-security.md)
- [“输出”窗口](../ide/reference/output-window.md)
- [跟踪和检测应用程序](/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)
- [C#、F# 和 Visual Basic 项目类型](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
