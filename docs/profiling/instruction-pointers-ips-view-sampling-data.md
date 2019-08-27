---
title: “指令指针”(IP) 视图 - 采样数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Instruction Pointers view
ms.assetid: c7f647bb-c5a3-4708-9f9d-33c0fd6e2e96
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 579887c22df16d555c3f309b4326740060aefc1f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442225"
---
# <a name="instruction-pointers-ips-view---sampling-data"></a>“指令指针”(IP) 视图 - 采样数据
采样数据的 IP 视图列出分析运行期间收集样本时直接执行的程序集指令的性能数据。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

|列|说明|
|------------|-----------------|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**模块名**|指令所在模块的名称。|
|**模块路径**|指令所在模块的路径。|
|**源文件**|指令所在的源文件。|
|**函数名**|指令所在函数的名称。|
|**函数行号**|此函数在源文件中的起始行号。|
|**函数地址**|函数在加载的二进制文件中的起始内存地址。|
|**源行开始**|源文件中收集此样本的的起始行号。|
|**源行结束**|源文件中收集此样本的的结束行号。|
|**源字符开始**|源文件行中收集此样本的起始字符的偏移量。|
|**源字符结束**|源文件行中收集此样本的结束字符的偏移量。|
|**指令地址**|指令在加载的二进制文件中的地址。|
|**独占样本数**|执行指令时收集的样本总数。|
|**独占样本数百分比**|执行指令时在分析运行期间收集的所有样本数的百分比。|

## <a name="see-also"></a>请参阅
- [“指令指针”(IP) 视图 - 采样](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)