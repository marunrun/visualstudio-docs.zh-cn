---
title: 调试器运行内存不足的服务 |Microsoft Docs
ms.date: 07/10/2019
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.debug_no_memory
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger
author: isadorasophia
ms.author: isgarcia
manager: caslan
ms.workload:
- multiple
ms.openlocfilehash: 05664ffd056f69215e6fb00d6d49a59382a3692f
ms.sourcegitcommit: da4079f5b6ec884baf3108cbd0519d20cb64c70b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67854014"
---
# <a name="debugger-services-running-out-of-memory"></a>调试器运行内存不足的服务
调试服务内存不足，导致终止调试会话。

## <a name="to-investigate-this-error-on-windows"></a>若要调查此错误在 Windows 上
- 在签入的进程内存关系图**诊断工具**窗口以查看目标应用程序出现在内存中的巨大增长。 如果是这样，使用**内存使用情况**工具来诊断什么是基础问题，请参阅[分析内存使用情况](../profiling/memory-usage.md)。

- 如果目标应用程序似乎在消耗大量内存，则使用**任务管理器**窗口以查看内存使用情况的 Visual Studio (devenv.exe) 工作进程 (msvsmon.exe)，或在 VS code (vsdbg.exe/vsdbg-ui.exe) 到确定如果调试器问题。 如果内存不足运行的进程 devenv.exe，请考虑减少运行的 Visual Studio 扩展的数量。

## <a name="see-also"></a>请参阅
- [博客文章：调试时分析 CPU 和内存](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)
- [有关内存管理](/windows/win32/memory/about-memory-management)
