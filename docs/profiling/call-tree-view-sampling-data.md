---
title: “调用关系树”视图 - 采样数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method,Call Tree view
- Call Tree view
ms.assetid: 5c4e8ec3-d0d3-485a-93bd-9060df4eb739
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d0655c0faf57a72d6e99ba65f9f84db059e5fe0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63406019"
---
# <a name="call-tree-view---sampling-data"></a>“调用树”视图 - 采样数据
“调用关系树”视图显示在分析应用程序中遍历的函数执行路径。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

 树的根是应用程序或组件的入口点。 每个函数节点都列出它调用的所有函数以及有关这些函数调用的性能数据。

 “调用关系树”视图中的值对应于调用树中父函数所调用的函数实例。 通过将函数实例值与分析运行中的样本总数进行对比得出百分比值。

## <a name="highlight-the-execution-hot-path"></a>突出显示执行热路径
 “调用关系树”视图可以展开并突出显示进程的执行路径或采样频率最高的函数。 若要显示最活跃的路径，请右键单击该进程或函数，然后单击“展开热路径”。

## <a name="set-the-call-tree-root-node"></a>设置调用树根节点
 分析运行中的每个进程均显示为根节点。 若要设置“调用关系树”视图的开始节点，请右键单击要设置为开始节点的节点，然后选择“设置根节点”。

 设置根节点后，将从视图中排除所选节点的子树之外的所有其他条目。 若要将根节点重置回原始节点，请在“调用树视图”窗口中右键单击并选择“重置根节点”。

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
|**级别**|此函数在调用树中的深度。 仅在 [VSPerfReport](../profiling/vsperfreport.md) 命令行报表中。|
|**独占样本数**|当调用树中的父函数调用此函数时，此函数中收集的样本数。 此数值不包括此函数调用的函数中收集的样本。|
|**独占样本数百分比**|调用树中的父函数调用此函数时，分析运行中属于此函数的独占样本的所有样本数的百分比。|
|**非独占样本数**|当调用树中的父函数调用此函数时，此函数中收集的样本数。 此数值包括此函数调用的函数中收集的样本。|
|**非独占样本数百分比**|调用关系树中的父函数调用此函数时，分析运行中属于此函数的非独占样本的所有样本数的百分比。|

## <a name="see-also"></a>请参阅
- [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)
- [“调用树”视图 - 探查器采样数据](../profiling/call-Tree-view-sampling-data.md)
- [“调用树”视图 - 采样](../profiling/call-tree-view-dotnet-memory-sampling-data.md)
- [“调用树”视图 - 检测](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)
- [“调用树”视图](../profiling/call-tree-view-instrumentation-data.md)