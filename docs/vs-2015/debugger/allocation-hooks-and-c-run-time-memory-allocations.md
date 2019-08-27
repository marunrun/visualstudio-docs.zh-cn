---
title: 分配挂钩和 C 运行时内存分配 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- debugging [C++], hook functions
- memory allocation, troubleshooting allocation hooks
- allocation hooks
- hooks, allocation
ms.assetid: cc34ee96-3d91-41bd-a019-aa3759139e7e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8487972c237b9c2ba6bf2594ffc1df43fa0c63cd
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65702426"
---
# <a name="allocation-hooks-and-c-run-time-memory-allocations"></a>分配挂钩和 C 运行时内存分配
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对分配挂钩函数的一个非常重要的限制是，当它们调用任何分配内部内存的 C 运行库函数时，必须显式忽略 `_CRT_BLOCK` 块（由 C 运行库函数内部进行的内存分配）。 可通过在分配挂钩函数起始包括如下代码来忽略 `_CRT_BLOCK` 块：  
  
```  
if ( nBlockUse == _CRT_BLOCK )  
    return( TRUE );  
```  
  
 如果您的分配挂钩未忽略 `_CRT_BLOCK` 块，那么挂钩中调用的任何 C 运行库函数都会使程序陷入无穷循环。 例如，`printf` 执行内部分配。 如果挂钩代码调用`printf`，则产生的分配将导致您的挂钩以再次，调用该基类将调用**printf**再次，依此类推，直到堆栈溢出。 如果需要报告 `_CRT_BLOCK` 分配操作，回避该限制的一种方法是，使用 Windows API 函数而不是 C 运行时函数来进行格式化和输出。 因为 Windows API 不使用 C 运行库堆，所以它们不会使您的分配挂钩陷入无穷循环。  
  
 如果检查运行时库源文件，则会看到默认的分配挂钩函数 **CrtDefaultAllocHook**（直接返回 **TRUE**）位于其自身的独立文件 DBGHOOK.C 中。 如果希望调用分配挂钩（即使分配是由在应用程序的 **main** 函数之前执行的运行时启动代码进行的），则可将此默认函数替换为你自己的一个函数，而不使用 [_CrtSetAllocHook](https://msdn.microsoft.com/library/405df37b-2fd1-42c8-83bc-90887f17f29d)。  
  
## <a name="see-also"></a>请参阅  
 [编写调试挂钩函数](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 示例](https://msdn.microsoft.com/21e1346a-6a17-4f57-b275-c76813089167)
