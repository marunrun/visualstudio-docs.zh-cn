---
title: “调用树”视图 - .NET 内存采样数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Call Tree view
ms.assetid: fbb6cb60-420b-4ca9-8306-2494f7d321fe
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7ed0d8a2ccf8e33b493ddcb71f9ce3a794a06862
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150745"
---
# <a name="call-tree-view---net-memory-sampling-data"></a>“调用树”视图 - .NET 内存采样数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“调用关系树”视图显示在分析应用程序中遍历的函数执行路径。 树的根是应用程序或组件的入口点。 每个函数节点都会列出它调用的所有函数以及有关这些函数调用的 .NET 内存分配数据。  
  
 “调用关系树”视图中的值对应于调用树中父函数所调用的函数实例。 通过将函数实例值与分析运行中的分配总数或大小进行对比计算出百分比值。  
  
## <a name="highlighting-the-execution-hot-path"></a>突出显示执行热路径  
 “调用树”视图可以展开并突出显示创建最大或最多内存对象的进程或函数的执行路径。 若要显示最活跃的路径，请右键单击该进程或函数，然后单击“展开热路径”  。  
  
## <a name="setting-the-call-tree-root-node"></a>设置调用树根节点  
 分析运行中的每个进程均显示为根节点。 若要将“调用树”视图的开始节点设置为其他节点，请右键单击要设置为开始节点的节点，然后选择“设置根”  。  
  
 设置根节点后，将从视图中排除所选节点的子树之外的所有其他条目。 可将根节点重置为刚才查看的节点，在“调用树”视图窗口中右键单击并选择“重置根”  。  
  
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
|**级别**|此函数在调用树中的深度。|  
|**非独占分配数**|调用树中父函数调用的此函数的实例所分配的对象数。 此数目包括子函数的分配数。|  
|**非独占分配数百分比**|分析运行期间创建的属于此函数的非独占分配的所有对象数的百分比。|  
|**独占分配数**|调用树中父函数调用的此函数的实例所分配的对象数。 此数目不包括子函数的分配数。|  
|**独占分配数百分比**|在分析运行期间创建的，由调用树中的父函数调用的函数实例的独占分配对象数的百分比。|  
|**非独占字节数**|调用树中父函数所调用的此函数的实例所分配的内存字节数。 此数目包括子函数的分配数。|  
|**非独占字节数百分比**|分析运行期间分配的属于此函数的非独占分配的所有内存字节数的百分比。|  
|**独占字节数**|调用树中父函数所调用的此函数的实例所分配的内存字节数。 此数目不包括子函数的分配数。|  
|**独占字节数百分比**|分析运行期间分配的属于此函数的独占分配的所有内存字节数的百分比。|  
  
## <a name="see-also"></a>另请参阅  
 ["调用关系树" 视图-检测](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)   
 [调用关系树视图](../profiling/call-tree-view-sampling-data.md)   
 [“调用关系树”视图](../profiling/call-tree-view-instrumentation-data.md)
