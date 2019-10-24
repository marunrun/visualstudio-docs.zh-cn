---
title: 调试器服务内存不足 |Microsoft Docs
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
ms.openlocfilehash: 12215f9c740e68c4f2749a51b06c09a1385dae1a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737843"
---
# <a name="debugger-services-running-out-of-memory"></a>调试器服务内存不足
调试服务内存不足，导致调试会话终止。

## <a name="to-investigate-this-error-on-windows"></a>在 Windows 上调查此错误
- 你可以在 "**诊断工具**" 窗口中查看 "处理内存" 关系图，以查看目标应用程序是否在内存中遇到巨大的增长。 如果是这样，请使用 "**内存使用率**" 工具来诊断基本问题，请参阅[分析内存使用情况](../profiling/memory-usage.md)。

- 如果目标应用程序似乎不占用大量内存，请使用 "**任务管理器**" 窗口来检查 Visual Studio （devenv）、工作进程（msvsmon）或 VS Code （vsdbg/vsdbg-ui）的内存使用情况，以确定这是否为调试器问题。 如果内存不足的进程是 devenv，请考虑减少运行的 Visual Studio 扩展的数目。

## <a name="see-also"></a>请参阅
- [博客文章：在调试时分析 CPU 和内存](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)
- [关于内存管理](/windows/win32/memory/about-memory-management)
