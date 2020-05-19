---
title: 分配挂钩函数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- memory allocation, logging allocation information
- insufficient memory
- debugging [C++], hook functions
- _CrtSetAllocHook function
- allocation hooks
- hooks, allocation
ms.assetid: 6bfbdb65-8cb1-4c21-8c45-7194a2b77c1e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f684c6c66448fdab2ee7607a81ff7ed769a5e607
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745824"
---
# <a name="allocation-hook-functions"></a>分配挂钩函数
每次分配、重新分配或释放内存时，都会调用通过 [_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook) 安装的分配挂钩函数。 这种挂钩可用于多种不同用途。 可用它测试应用程序处理内存不足情况的方式，例如检查分配模式，或记录分配信息以供将来分析。

> [!NOTE]
> 注意有关在分配挂钩函数中使用 C 运行库函数的限制，详见[分配挂钩和 C 运行时内存分配](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)中的说明。

 分配挂钩函数应具有类似于以下示例的原型：

```cpp
int YourAllocHook(int nAllocType, void *pvData,
        size_t nSize, int nBlockUse, long lRequest,
        const unsigned char * szFileName, int nLine )
```

 传递给 [_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook) 的指针为 _CRT_ALLOC_HOOK 类型，如 CRTDBG.H 中所定义：

```cpp
typedef int (__cdecl * _CRT_ALLOC_HOOK)
    (int, void *, size_t, int, long, const unsigned char *, int);
```

 当运行时库调用挂钩时，nAllocType 参数指示即将进行的分配操作（ **_HOOK_ALLOC**， **_HOOK_REALLOC** 或 **_HOOK_FREE**)。 在释放或重新分配中，`pvData` 具有一个指向即将释放的块的用户文章的指针。 但是，对于分配，该指针为空，因为分配尚未发生。 其余参数包含所讨论的分配大小、其块类型、与其相关联的顺序请求编号以及指向文件名的指针。 如果可用，参数还包括在其中进行分配的行号。 挂钩函数执行完毕其作者需要的任何分析和其他任务后，它必须返回 TRUE，表示分配操作可以继续，或者返回 FALSE，表示操作会失败。 此类型的简单挂钩可以检查到目前为止分配的内存量，如果内存量超过了小限制，则返回 FALSE。 然后，应用程序会遇到通常只有在可用内存非常低时才会出现的分配错误。 较复杂的挂钩可以跟踪分配模式，分析内存使用，或在特定情况发生时进行报告。

## <a name="see-also"></a>请参阅

- [分配挂钩和 C 运行时内存分配](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)
- [编写调试挂钩函数](../debugger/debug-hook-function-writing.md)