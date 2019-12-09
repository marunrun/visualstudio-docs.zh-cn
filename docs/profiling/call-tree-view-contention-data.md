---
title: “调用树”视图 - 争用数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Call Tree view
ms.assetid: 9bd4bde2-2ca3-446c-9ccc-7421522e03ae
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: e91e231f72b006d2020c8b4d5d96c7e24fa1dd9c
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779774"
---
# <a name="call-tree-view---contention-data"></a>“调用树”视图 - 争用数据
“调用关系树”视图显示在分析应用程序中遍历的函数执行路径。 树的根是应用程序或组件的入口点。 每个函数节点都列出它所调用的所有函数、函数被阻止的次数，以及函数由于与其他线程或进程争用资源而被阻止的时间量。

 “调用关系树”视图中的值对应于调用树中父函数所调用的函数实例。 通过将函数实例值与分析运行中的争用总数进行对比得出百分比值。

## <a name="highlight-the-execution-hot-path"></a>突出显示执行热路径
 “调用树”视图可以展开并突出显示进程的执行路径或创建最多争用的函数。

- 若要显示最活跃的路径，请右键单击该进程或函数，然后单击“展开热路径”  。

## <a name="set-the-call-tree-root-node"></a>设置调用树根节点
 分析运行中的每个进程均显示为根节点。 若要设置“调用关系树”视图的开始节点，请右键单击要设置为开始节点的节点，然后单击“设置根节点”  。

 设置根节点后，将从视图中排除所选节点的子树之外的所有其他条目。 若要将根节点重置回原始节点，可在“调用树”视图中右键单击，然后单击“重置根节点”  。

|列|说明|
|------------|-----------------|
|**独占阻塞的时间**|阻止此执行路径中此函数的实例在分析运行中执行的时间。 此时间不包括此函数调用的子函数的阻塞时间。|
|**独占阻塞的时间百分比**|此执行路径中此函数的独占阻塞时间占分析运行中的所有阻塞时间的百分比。|
|**独占争用**|在此执行路径中此函数的实例中发生的争用次数。 此次数不包括此函数调用的子函数的争用数。|
|**独占争用数百分比**|调用树中的父函数调用此函数时，分析运行中属于此函数实例的独占争用的所有争用的百分比。|
|**函数地址**|函数的地址。|
|**函数名**|该函数的完全限定名。|
|**非独占阻塞的时间**|阻止此执行路径中此函数的实例在分析运行中执行的总时间。 此时间包括此函数调用的子函数的阻塞时间。|
|**非独占阻塞的时间百分比**|此执行路径中此函数实例的非独占阻塞时间占分析运行中的所有阻塞时间的百分比。|
|**非独占争用**|在此执行路径中阻止此函数实例的争用总次数。 此次数包括此函数调用的子函数的争用数。|
|**非独占争用数百分比**|此执行路径中此函数实例的非独占争用占分析运行中的所有争用的百分比。|
|**级别**|此函数在调用树中的级别。 仅在 VSReport 命令行报表中。 有关详细信息，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。|
|**函数行号**|此函数在源文件中的起始行号。|
|**模块名**|函数所在模块的名称。|
|**模块路径**|函数所在模块的路径。|
|**进程 ID**|分析运行的进程 ID (PID)。|
|**进程名**|进程的名称。|
|**源文件**|此函数的定义所在的源文件。|

## <a name="see-also"></a>请参阅
- [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)
- [“调用树”视图](../profiling/call-tree-view.md)
- [“调用树”视图 - 检测](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)
- [“调用树”视图 - 采样](../profiling/call-tree-view-dotnet-memory-sampling-data.md)
- [“调用树”视图](../profiling/call-tree-view-instrumentation-data.md)
- [“调用树”视图](../profiling/call-tree-view-sampling-data.md)
