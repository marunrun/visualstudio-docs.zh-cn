---
title: “行”视图 — 争用数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Lines view
ms.assetid: 859b02d2-eddf-4ad3-95de-0df67ee2ab03
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1dfcdf67c897c0c1565e536a69cc940b9df83390
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778591"
---
# <a name="lines-view---contention-data"></a>“行”视图 - 争用数据
争用数据的“行”视图列出分析运行期间收集样本时所执行语句的性能数据。 在源文件中，一个语句可分散在多行中，而一行也可包括多个语句。

 语句由以下数据标识：

- 包含函数语句的源文件。

- 包含该语句的函数。

- 该语句的起始源代码行。

- 该语句的起始源代码行中的字符。

- 该语句的结束源代码行。

- 该语句的结束源代码行中的字符。

  “行名”列提供一串可排序的标识符数据。

  下表介绍“行视图”报告中的各列。

|列|说明|
|------------|-----------------|
|**独占阻塞的时间**|因争用事件而阻滞此语句执行语句中代码的时间长度。 不包括语句所调用的函数中的阻塞时间。|
|**独占阻塞的时间百分比**|语句的独占阻塞时间占进程中所有阻塞时间的百分比。|
|**独占争用**|因争用事件而阻滞此语句执行语句中代码的次数。 不包括语句所调用函数中的争用事件数。|
|**独占争用数百分比**|此语句的独占争用数占进程中所有争用事件数的百分比。|
|**函数地址**|此语句所在函数的地址。|
|**函数名**|此语句所在函数的完全限定名称。|
|**非独占阻塞的时间**|此语句及其中所调用各个函数中的阻塞时间。|
|**非独占阻塞的时间百分比**|语句的非独占阻塞时间占进程中所有阻塞时间的百分比。|
|**非独占争用**|阻滞此语句及其中所调用函数执行的次数。|
|**非独占争用数百分比**|此语句的非独占争用数占进程中所有争用事件数的百分比。|
|**行名**|由探查器生成的行标识符。 标识符使用以下语法：`SourceFile` **;[** `LineNumberStart` **,** `CharacterStart` **]->;[** `LineNumberEnd` **,** `CharacterEnd` **]**|
|**函数行号**|此函数在源文件中的起始行号。|
|**模块名**|语句所在模块的名称。|
|**模块路径**|语句所在模块的路径。|
|**进程 ID**|所分析进程的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**源字符开始**|此语句的起始源文件行中起始字符的偏移量。|
|**源字符结束**|此语句的结束源文件行中起始字符的偏移量。|
|**源文件**|函数语句所在源文件的名称。|
|**源行开始**|该语句在源文件中的起始行号。|
|**源行结束**|该语句在源文件中的结束行号。|

## <a name="see-also"></a>请参阅
- [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)
- [“行”视图](../profiling/lines-view.md)
- [“行”视图 - 采样](../profiling/lines-view-dotnet-memory-sampling-data.md)
- [“行”视图](../profiling/lines-view-sampling-data.md)
