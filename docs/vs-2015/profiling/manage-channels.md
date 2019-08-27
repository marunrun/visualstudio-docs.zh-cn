---
title: 管理通道 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.tools.managechannels
helpviewer_keywords:
- Concurrency Visualizer, Manage Channels
ms.assetid: 507b06e9-bb56-4a72-8fd5-f91f958da6fc
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 894378d6648139b7ec2b587eb0066a5725af7a71
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443721"
---
# <a name="manage-channels"></a>管理通道
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在并发可视化工具的“线程视图”中，可以整理进程的各个通道，以便查看特定模式。 您可以将通道排序、上下移动，以及隐藏或显示这些通道。  
  
## <a name="sort-by"></a>排序依据  
 基于当前的缩放级别，您可以使用“排序依据”控件按不同的条件对线程排序。 在查找特定模式时，这特别有用。 您可以按照以下条件排序：  
  
|条件|定义|  
|--------------|----------------|  
|开始时间|按线程的开始时间排序。 这是默认的排序顺序。|  
|结束时间|按线程的结束时间排序。|  
|执行|按执行所用的时间百分比对线程排序。|  
|同步|按同步所用的时间百分比对线程排序。|  
|I/O|按 I/O（读取和写入数据）所用的时间百分比对线程排序。|  
|休眠|按休眠所用的时间百分比对线程排序。|  
|分页|按分页所用的时间百分比对线程排序。|  
|优先|按抢占所用的时间百分比对线程排序。|  
|UI 处理|按用户界面处理所用的时间百分比对线程排序。|  
  
## <a name="move-selected-channel-up-or-down"></a>上移或下移选定的通道  
 可以使用这些控件向上或向下移动列表中的通道。 例如，您可以将彼此相关的通道放在一起，以便帮助您检查特定的模式或跨线程关系。  
  
## <a name="move-selected-channel-to-top-or-bottom"></a>将选定的通道移动到顶部或底部  
 您可以将选定的通道移动到列表的顶部或底部，以便检查特定的模式，或在检查某些通道时移开其他的通道。  
  
## <a name="hide-selected-channels"></a>隐藏选定的通道  
 如果要隐藏通道，请选择此控件。 例如，如果一个线程在您托管进程的生存期内 100% 同步，则可以在分析其他线程时隐藏该线程。  
  
> [!NOTE]
> 隐藏某个线程时，还会将其从计算时间中移除，计算时间显示在活动图例和分析报告中。  
  
## <a name="show-all-channels"></a>显示所有通道  
 当一个或多个通道被隐藏时，此控件处于活动状态。 如果选择此控件，将显示所有隐藏的元素并将其全部添加回时间计算。  
  
## <a name="move-markers-to-top"></a>将标记移到顶部  
 如果跟踪包含标记事件，则可以使用此命令将标记通道移动到时间线的顶部。 它们的相对顺序将被保留。  
  
## <a name="group-markers-by-thread"></a>按线程对标记进行分组  
 如果跟踪包含标记事件，则可以使用此命令，按照生成标记事件的线程对标记通道进行分组。  磁盘通道将被移动到列表的顶部，而 GPU 通道将被移动到底部。  
  
## <a name="see-also"></a>请参阅  
 [缩放控件（线程视图）](../profiling/zoom-control-threads-view.md)   
 [打开/关闭度量模式](../profiling/measure-mode-on-off.md)   
 [“线程”视图](../profiling/threads-view-parallel-performance.md)
