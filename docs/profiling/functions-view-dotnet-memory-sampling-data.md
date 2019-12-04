---
title: “函数”视图 - .NET 内存采样数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Functions view
ms.assetid: 5d9c6302-2ffd-430e-9535-13ce795f9f7c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: cce13da0c2dfee61d70da8bc288d1f0ff4690deb
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74780034"
---
# <a name="functions-view---net-memory-sampling-data"></a>“函数”视图 - .NET 内存采样数据
使用采样方法收集的 .NET 内存分配分析数据的“函数”视图会列出分析运行期间分配内存的函数，并报告分配的大小和数量。

|列|说明|
|------------|-----------------|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**模块名**|函数所在模块的名称。|
|**模块路径**|函数所在模块的路径。|
|**源文件**|此函数的定义所在的源文件。|
|**函数名**|该函数的完全限定名。|
|**函数行号**|此函数在源文件中的起始行号。|
|**函数地址**|函数的地址。|
|**非独占分配数**|此函数及其子函数中分配的对象总数。|
|**非独占分配数百分比**|分析运行期间分配的属于此函数的非独占分配的所有对象数的百分比。|
|**独占分配数**|在调用堆栈顶部直接执行函数时创建的对象数。 此数目不包括在子函数中创建的对象。|
|**独占分配数百分比**|分析运行期间分配的属于此函数的独占分配的所有对象数的百分比。|
|**非独占字节数**|此函数及其子函数分配的内存字节数。|
|**非独占字节数百分比**|分析运行期间分配的属于此函数的非独占字节的所有内存字节数的百分比。|
|**独占字节数**|此函数而非其子函数分配的内存字节数。|
|**独占字节数百分比**|分析运行期间分配的属于此函数的独占字节的所有内存字节数的百分比。|

## <a name="see-also"></a>请参阅
- [“函数”视图 - 检测](../profiling/functions-view-dotnet-memory-instrumentation-data.md)
- [“函数”视图](../profiling/functions-view-sampling-data.md)
- [“函数”视图](../profiling/functions-view-instrumentation-data.md)
