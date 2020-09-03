---
title: “模块”视图 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.modules
helpviewer_keywords:
- Modules view
- profiling tools reports, Modules view
- profiling tools, Modules view
ms.assetid: 4314a404-2120-425b-be42-180cd4bac840
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d396aec92b43aebca9b398c6d481962138354e0e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195602"
---
# <a name="modules-view"></a>“模块”视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“模块”视图列出分析数据的模块。 每个模块是一个层次结构树的根节点。 模块的分析函数在模块节点下列出。 如果分析数据是使用采样方法收集的，则行信息在函数节点下列出，指令指针数据在行节点下列出。  
  
 展开或折叠模块名称可显示或关闭模块性能数据的视图。  
  
 若要添加和删除列，请在报告窗口中单击鼠标右键，然后选择“添加/删除列”  。 可以通过单击列名对数据进行排序。 有关详细信息，请参阅 [如何：自定义报表视图列](../profiling/how-to-customize-report-view-columns.md)。  
  
 “模块”视图中的可用列取决于用于收集数据的分析方法（采样法或检测法）以及是否在分析运行期间收集 .NET 内存数据。  
  
## <a name="see-also"></a>另请参阅  
 [模块视图](../profiling/modules-view-sampling-data.md)   
 [模块视图](../profiling/modules-view-instrumentation-data.md)   
 ["模块" 视图-检测](../profiling/modules-view-dotnet-memory-instrumentation-data.md)   
 ["模块" 视图-采样](../profiling/modules-view-dotnet-memory-sampling-data.md)   
 [“模块”视图](../profiling/modules-view-contention-data.md)
