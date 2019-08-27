---
title: 客户端块挂钩函数 |Microsoft Docs
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
- client blocks, validating and reporting data
- debugging [C++], hook functions
- _CrtSetDumpClient function
- client blocks, hook functions
- hooks, client block
ms.assetid: f21c197e-565d-4e3f-9b27-4c018c9b87fc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 900e8db238ee26e0a7015c2acc1741a1917c8cb3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62564068"
---
# <a name="client-block-hook-functions"></a>客户端块挂钩函数
如果想要验证或报告存储在 `_CLIENT_BLOCK` 块中的数据的内容，可以专为此目的编写函数。 如同 CRTDBG.H 中所定义的，所编写的函数必须有与下面类似的原型：

```cpp
void YourClientDump(void *, size_t)
```

 换句话说，挂钩函数应接受一个 void 指针（指向分配块的起始），以及一个 size_t 类型值（指示分配大小），并返回 `void`。 除此之外，其内容由您决定。

 使用 [_CrtSetDumpClient](/cpp/c-runtime-library/reference/crtsetdumpclient) 安装了挂钩函数后，每次转储 `_CLIENT_BLOCK` 块时都将调用该挂钩函数。 然后，可以使用 [_CrtReportBlockType](/cpp/c-runtime-library/reference/crtreportblocktype) 获取有关转储块的类型或子类型的信息。

 传递给 `_CrtSetDumpClient` 的指向函数的指针是 _CRT_DUMP_CLIENT 类型，如 CRTDBG.H 中所定义：

```cpp
typedef void (__cdecl *_CRT_DUMP_CLIENT)
   (void *, size_t);
```

## <a name="see-also"></a>请参阅

- [编写调试挂钩函数](../debugger/debug-hook-function-writing.md)
- [crt_dbg2 示例](https://msdn.microsoft.com/library/21e1346a-6a17-4f57-b275-c76813089167)
- [_CrtReportBlockType](/cpp/c-runtime-library/reference/crtreportblocktype)