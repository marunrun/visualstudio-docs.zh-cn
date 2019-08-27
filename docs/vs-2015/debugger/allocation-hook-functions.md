---
title: 分配挂钩函数 |Microsoft Docs
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
- memory allocation, logging allocation information
- insufficient memory
- debugging [C++], hook functions
- _CrtSetAllocHook function
- allocation hooks
- hooks, allocation
ms.assetid: 6bfbdb65-8cb1-4c21-8c45-7194a2b77c1e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 81135546ffa208a4efb96569cd7968dfe560cdf9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65702528"
---
# <a name="allocation-hook-functions"></a>分配挂钩函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分配挂钩函数，使用安装[_CrtSetAllocHook](https://msdn.microsoft.com/library/405df37b-2fd1-42c8-83bc-90887f17f29d)，每次分配、 重新分配或释放内存时调用。 该类型的挂钩可用于很多不同用途。 例如，可用它测试应用程序处理内存不足情况的方式，检查分配模式，或记录分配信息以供将来分析。  
  
> [!NOTE]
> 注意有关在分配挂钩函数中使用 C 运行库函数的限制，详见[分配挂钩和 C 运行时内存分配](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)中的说明。  
  
 分配挂钩函数应有类似下面的原型：  
  
```  
int YourAllocHook(int nAllocType, void *pvData,  
        size_t nSize, int nBlockUse, long lRequest,  
        const unsigned char * szFileName, int nLine )  
```  
  
 传递给 [_CrtSetAllocHook](https://msdn.microsoft.com/library/405df37b-2fd1-42c8-83bc-90887f17f29d) 的指针为 _CRT_ALLOC_HOOK 类型，如 CRTDBG.H 中所定义：  
  
```  
typedef int (__cdecl * _CRT_ALLOC_HOOK)  
    (int, void *, size_t, int, long, const unsigned char *, int);  
```  
  
 当运行库调用您的挂钩*nAllocType*参数用于指示哪些分配即将执行的操作 (**_HOOK_ALLOC**， **_HOOK_REALLOC**，或 **_HOOK_FREE**)。 在释放或重新分配的情况下，`pvData` 包含指向将释放块的用户主题的指针。 但在分配情况下，该指针为空，因为分配尚未发生。 剩余的参数包含所讨论分配的大小、其块类型、与它关联的顺序请求编号，以及指向在其中进行分配的文件名和行号的指针（如果有）。 挂钩函数在执行完所有分析及需要做的其他任务后，它必须返回 **TRUE**，表明分配操作可以继续，或返回**FALSE**，表明分配操作会失败。 一个此类型的简单挂钩函数可能会检查到目前为止分配的内存量，如果该内存量超出最小限制，则返回**FALSE**。 然后应用程序将遇到内存分配错误，这种错误通常只会在可用内存极为不足时发生。 较复杂的挂钩函数可以跟踪分配模式，分析内存使用，或在特定情况发生时进行报告。  
  
## <a name="see-also"></a>请参阅  
 [分配挂钩和 C 运行时内存分配](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)   
 [编写调试挂钩函数](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 示例](https://msdn.microsoft.com/21e1346a-6a17-4f57-b275-c76813089167)
