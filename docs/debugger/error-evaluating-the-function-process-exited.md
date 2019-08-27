---
title: 错误：目标进程已退出，代码&#39;代码&#39;对函数求值时&#39;函数&#39;|Microsoft Docs
ms.date: 4/06/2018
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.process_exit_during_func_eval
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 75d82b6011a0dfa7f2c388e7d5f39a9ebabcd663
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62850816"
---
# <a name="error-the-target-process-exited-with-code-39code39-while-evaluating-the-function-39function39"></a>错误：目标进程已退出，代码&#39;代码&#39;对函数求值时&#39;函数&#39;

完整的消息文本：目标进程退出代码为 code 评估函数 function 时。

为更轻松地检查 .NET 对象的状态，调试器会自动强制调试的进程运行其他代码（通常是属性 getter 方法和`ToString`函数）。 在大多数情况下，这些函数会成功完成或引发可由调试器捕获的异常。 但是，在某些情况下，由于异常跨越内核边界、需要用户消息循环或不可恢复，因此无法捕获。 结果，执行代码的属性 getter 或 ToString 方法或者显式终止进程 (例如，调用`ExitProcess()`) 或引发不能被捕获的未经处理异常 (例如， `StackOverflowException`)，从而终止调试的进程并结束调试会话。 如果你遇到此错误消息，就是发生了这个问题。

此问题的一个常见原因是，当调试器计算调用自身的属性时，可能会导致堆栈溢出异常。 堆栈溢出异常无法恢复，目标进程将终止。

## <a name="to-correct-this-error"></a>更正此错误

此问题有两个可能的解决方案。

### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>解决方法 #1:防止调试器调用 getter 的属性或 ToString 方法 

错误消息将告诉你调试器尝试调用的函数的名称。 使用此函数的名称，你可以尝试从**即时**窗口重新计算该函数以调试该求值。 从**即时**窗口求值可以进行调试，因为与**自动/局部变量/监视**窗口的隐式求值不同，调试器将在未经处理的异常处中断。

如果可以修改此函数，可以阻止调试器调用 getter 属性或`ToString`方法。 请尝试以下方法之一：

* 将方法更改为除 getter 属性或 ToString 方法之外的其他类型的代码，问题将会消失。
    或
* （对于 `ToString`） 为类型定义 `DebuggerDisplay` 特性，调试器将计算 `ToString` 之外的值。
    或
* （对于属性 getter）为属性定义 `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` 特性。 如果您的方法因为 API 兼容性而要保留属性，这很有用，但它应该真是一个方法。

如果您不能修改此方法，您可以在备用的指令处中断目标进程，然后重试求值。

### <a name="solution-2-disable-all-implicit-evaluation"></a>解决方案 2:禁用所有隐式计算

如果先前的解决方案未解决此问题，请转到**工具** > **选项**，并取消选中调试 > 常规 > 启用属性求值和其他隐式函数调用设置。 这将会禁用大多数隐式函数求值，应该会解决此问题。
