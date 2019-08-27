---
title: “调用方 - 被调用方”视图 - 采样数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method,Caller/Callee view
- Caller/Callee view
ms.assetid: 28e85ed5-1512-4b59-bb84-138a2abca7dd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8f1d0cd651eac9f6f05acccd233d1741e624f5e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63405890"
---
# <a name="callercallee-view---sampling-data"></a>“调用方/被调用方”视图 - 采样数据
“调用方/被调用方”视图显示所选函数及其父函数和子函数的分析信息。 “调用方/被调用方”视图包含三个网格。

 **当前函数**在中间网格中显示，其显示所选函数的分析信息。 这些值包括对函数的所有采样调用。

 **调用当前函数的函数**在顶部网格中显示，其显示调用方（父）函数对所选（当前）函数的值的各个调用。

 **由当前函数调用的函数**在底部网格中显示，当前函数调用子函数时，它会显示所选函数的被调用方（子）函数的分析信息。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

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
|**Type**|函数的上下文：<br /><br /> -   **0** - 当前函数<br />-   **1** - 调用当前函数的函数<br />-   **2** - 当前函数调用的函数|
|**根函数名**|当前函数的名称。|
|**非独占样本数**|-   对于当前函数，非独占样本数是所收集的样本数，尽管当时正在执行此函数或其中一个子函数。<br />-   对于调用方函数，非独占样本数是此函数调用当前函数时收集的当前函数的非独占样本数。<br />-   对于被调用方函数，非独占样本数当前函数调用此函数时收集的此函数的非独占样本数。|
|**非独占样本数百分比**|分析运行中属于此函数的非独占样本的所有样本数的百分比。|
|**独占样本数**|-   对于当前函数，独占样本数是直接执行此函数时（即此函数位于调用堆栈顶部时）收集的分析运行中的样本数。 此函数的子函数执行时收集的样本不会计入独占样本数。<br />-   对于调用方函数，是此函数调用当前函数时收集的当前函数的独占样本数。<br />-   对于被调用方函数，独占样本数是当前函数调用此函数时收集的此函数的独占样本数。|
|**独占样本数百分比**|分析运行中属于此函数的独占样本的所有样本数的百分比。|

## <a name="see-also"></a>请参阅
- [“调用方/被调用方”视图 - .NET 内存采样数据](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)
- [“调用方/被调用方”视图 - .NET 内存检测数据](../profiling/caller-callee-view-net-memory-instrumentation-data.md)
- [“调用方/被调用方”视图 - 检测数据](../profiling/caller-callee-view-instrumentation-data.md)