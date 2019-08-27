---
title: “模块”视图 - 采样数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Modules view
- sampling profiling method,Modules view
ms.assetid: 816f5633-65d7-41e5-aee1-033628d4e2df
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5c3aa55bfc521521e28686ebb248053350ae14a7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438917"
---
# <a name="modules-view---sampling-data"></a>“模块”视图 - 采样数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

采样数据的“模块”视图显示按分析数据中采样的模块分组的性能数据。 每个模块都是一个层次结构树的根。 模块的采样函数在模块节点下列出。  
  
> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
  
 如果在收集样本时执行函数（即函数处于调用堆栈顶部），则执行的源行和指令地址在函数节点下列出。 因为在执行行或指令时会为源行或指令指针收集数据，所以非独占和独占值对于行数据和指令数据始终是相同的。  
  
|列|说明|  
|------------|-----------------|  
|**名称**|模块、函数、行号或指令指针地址的名称。|  
|**进程 ID**|分析运行的进程 ID (PID)。|  
|**进程名**|进程的名称。|  
|**模块名**|包含函数、行或指令指针的模块的名称。|  
|**模块路径**|包含模块、函数、行或指令指针的模块的路径。|  
|**源文件**|此函数的定义所在的源文件。|  
|**函数行号**|此函数在源文件中的起始行号。|  
|**非独占样本数**|-   对于函数，是在其中执行此函数或此函数调用的函数的样本的数量；即，包含此函数的调用堆栈样本的数量。<br />-   对于模块，是在其中执行此模块中的至少一个函数的样本的数量。<br />-   对于行或指令，是在其中执行此行或指令的样本的数量。|  
|**非独占样本数百分比**|-   对于函数或模块，是分析运行期间属于此函数或模块的非独占样本的所有样本数的百分比。<br />-   对于行或指令，是分析运行期间在其中执行此行或指令的所有样本数的百分比。|  
|**独占样本数**|-   对于函数，是在其中直接执行此函数的调用堆栈样本的数量；即，在其中此函数处于调用堆栈顶部的样本的数量。<br />-   对于模块，是此模块中函数的独占样本之和。<br />-   对于行或指令，是在其中执行此行或指令的样本的数量。|  
|**独占样本数百分比**|-    对于函数或模块，是分析运行期间属于此函数或模块的独占样本的所有样本数的百分比。<br />-   对于行或指令，是分析运行期间在其中执行此行或指令的所有样本数的百分比。|  
  
## <a name="see-also"></a>请参阅  
 [“模块”视图 - 采样](../profiling/modules-view-dotnet-memory-sampling-data.md)   
 [“模块”视图 - 检测](../profiling/modules-view-dotnet-memory-instrumentation-data.md)   
 [“模块”视图](../profiling/modules-view-instrumentation-data.md)
