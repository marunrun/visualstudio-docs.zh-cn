---
title: “指令指针”(IP) 视图 — 争用数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Instruction Pointers view
ms.assetid: f5e49c24-d4cf-4f87-977d-37e3223d1196
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d41f48594e50e9d5ae0c6f67aabab673a9f112a3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62995390"
---
# <a name="instruction-pointers-ips-view---contention-data"></a>“指令指针”(IP) 视图 — 争用数据
争用数据的 IP 视图列出分析运行期间被阻止执行的程序集指令的数据。

 下表说明“指令指针”视图中各列的值。

|列|说明|
|------------|-----------------|
|**独占阻塞的时间**|该函数中的阻塞时间。|
|**独占阻塞的时间百分比**|执行指令时的阻塞时间所占的百分比。|
|**独占争用**|执行指令时发生的争用次数。|
|**独占争用数百分比**|执行指令时发生的争用占分析运行期间所有争用的百分比。|
|**函数地址**|函数在加载的二进制文件中的起始内存地址。|
|**函数名**|指令所在函数的名称。|
|**指令地址**|指令在加载的二进制文件中的内存地址。|
|**函数行号**|此函数在源文件中的起始行号。|
|**模块名**|指令所在模块的名称。|
|**模块路径**|指令所在模块的路径。|
|**进程 ID**|所分析进程的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**源字符开始**|此指令的起始源文件行的字符偏移量。|
|**源字符结束**|此指令的结束源文件行的字符偏移量。|
|**源文件**|指令所在的源文件。|
|**源行开始**|此指令在源文件中的起始行号。|
|**源行结束**|此指令在源文件中的结束行号。|

## <a name="see-also"></a>请参阅
- [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)
- [“指令指针”(IP) 视图](../profiling/instruction-pointers-ips-view.md)
- [“指令指针”(IP) 视图 - 采样](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)
- [“指令指针”(IP) 视图](../profiling/instruction-pointers-ips-view-sampling-data.md)