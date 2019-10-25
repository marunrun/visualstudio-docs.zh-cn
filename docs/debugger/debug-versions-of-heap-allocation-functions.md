---
title: 堆分配函数的调试版本 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- _CRTDBG_MAP_ALLOC macro
- debugging [CRT], heap allocation functions
- debugging memory leaks, CRT debug library functions
- malloc function
- memory leaks, CRT debug library functions
- heap allocation, debug
- _malloc_dbg function
ms.assetid: 91748bdc-f4cd-4d8b-ab98-0493dab7ed0d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d0fde776e9f2bd48aca92c7ba6d7f1fe1e23f01a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738369"
---
# <a name="debug-versions-of-heap-allocation-functions"></a>堆分配函数的“Debug”版本
C 运行库包含堆分配函数的特殊“Debug”版本。 这些函数的名称与发行版本相同，只是追加了“_dbg”。 本主题用 `malloc` 和 `_malloc_dbg` 作为示例，描述 CRT 函数的发行版本和 _dbg 版本之间的差异。

 定义 [_DEBUG](/cpp/c-runtime-library/debug) 时，CRT 会将所有 [malloc](/cpp/c-runtime-library/reference/malloc) 调用映射到 [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg)。 因此，在调试时，无需使用 `_malloc_dbg` 代替 `malloc` 重写代码即可获得优势。

 但您可能希望显式调用 `_malloc_dbg`。 显式调用 `_malloc_dbg` 具有一些附加的好处：

- 跟踪 `_CLIENT_BLOCK` 类型分配。

- 存储分配请求所在的源文件和行号。

  如果不希望将 `malloc` 调用转换为 `_malloc_dbg`，则可以通过定义 [_CRTDBG_MAP_ALLOC](/cpp/c-runtime-library/crtdbg-map-alloc) 来获取源文件信息，这会使预处理器直接将对 `malloc` 的所有调用映射到 `_malloc_dbg`，而不是依赖于 `malloc` 周围的包装器。

  若要跟踪客户端块中各种类型的分配，必须直接调用 `_malloc_dbg`，并将 `blockType` 参数设置为 `_CLIENT_BLOCK`。

  未定义 _DEBUG 时，对 `malloc` 的调用不会受干扰，对 `_malloc_dbg` 的调用则解析为 `malloc`，同时会忽略 [_CRTDBG_MAP_ALLOC](/cpp/c-runtime-library/crtdbg-map-alloc) 的定义，并且不会提供与分配请求相关的源文件信息。 由于 `malloc` 没有块类型参数，因此对 `_CLIENT_BLOCK` 类型的请求会作为标准分配处理。

## <a name="see-also"></a>请参阅

- [CRT 调试方法](../debugger/crt-debugging-techniques.md)