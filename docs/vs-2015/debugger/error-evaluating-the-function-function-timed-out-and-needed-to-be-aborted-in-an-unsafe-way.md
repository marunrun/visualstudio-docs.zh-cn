---
title: 错误：对函数求值&#39;函数&#39;超时，需要以不安全的方式中止 |Microsoft Docs
ms.date: 11/15/2016
ms.topic: reference
f1_keywords:
- vs.debug.error.unsafe_func_eval_abort
ms.assetid: 0a9f70ed-21ad-4a10-8535-b9c5885ad8f4
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5d5a992751e31f21a7875091b4c8b1be9bd0bd0a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197062"
---
# <a name="error-evaluating-the-function-39function39-timed-out-and-needed-to-be-aborted-in-an-unsafe-way"></a>错误：对函数求值&#39;函数&#39;超时，需要以不安全的方式中止
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

完整的消息文本：评估函数 function 超时，需要以不安全的方式中止。 这可能会损坏目标进程。 

为了更加轻松地检查 .NET 对象的状态，调试器将自动强制调试的进程运行其他代码（通常是属性 getter 方法和 ToString 函数）。 在大多数情况下，这些函数快速完成，使调试更容易。 但是，调试器不会在沙盒中运行应用程序。 因此，属性 getter 或调入挂起的本机函数的 ToString 方法可能会导致无法恢复的长超时。 如果遇到此错误消息，说明发生了这种情况。
 
此问题的一个常见原因是：当调试器计算属性时，它只允许要检查的线程执行。 因此如果该属性等待其他线程在被调试的应用程序内运行，并且 .NET 运行时不能中断这种等待，此问题就会发生。
 
## <a name="to-correct-this-error"></a>更正此错误
 
此问题有三种可能的解决方案。
 
### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>解决方法 #1:防止调试器调用 getter 的属性或 ToString 方法
 
错误消息将告知调试器尝试调用的函数的名称。 如果可以修改此函数，您可以防止调试器调用属性 getter 或 ToString 方法。 请尝试以下方法之一：
 
* 将方法更改为除 getter 属性或 ToString 方法之外的其他类型的代码，问题将会消失。
    或
* （对于 ToString）在类型上定义 DebuggerDisplay 特性（attribute），调试器可以计算 ToString 以外的值。
    或
* （对于 getter 属性）在属性上定义 `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` 特性 (attribute)。 如果因为 API 兼容性原因而需要让一个方法保持为属性，这很有用。
 
### <a name="solution-2-have-the-target-code-ask-the-debugger-to-abort-the-evaluation"></a>解决方案 2:已请求中止计算在调试器的目标代码
 
错误消息将告知调试器尝试调用的函数的名称。 如果属性 getter 或 ToString 方法有时无法正确运行，尤其是在需要另一个线程来运行此代码的情况下，实现函数可以调用`System.Diagnostics.Debugger.NotifyOfCrossThreadDependency` 以便让调试器中止函数求值。 使用此解决方案，仍可以显式计算这些函数，但默认行为是在出现 NotifyOfCrossThreadDependency 调用时停止执行。
 
### <a name="solution-3-disable-all-implicit-evaluation"></a>解决方案 3:禁用所有隐式计算
 
如果先前的解决方案未解决此问题，请转到*工具* / *选项*，并取消选中调试   / 常规   / 启用属性求值和其他隐式函数调用设置  。 这将会禁用大多数隐式函数求值，应该会解决此问题。
