---
title: “调用树”视图 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.calltree
helpviewer_keywords:
- Call Tree view
- profiling tools reports, Call Tree view
- performance reports, Call Tree view
- profiling tools, Call Tree view
ms.assetid: b2dbc033-bf95-4d10-8e51-f9462979133e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0c28ef62629011b222ae1a846c04cbf4cdff17d3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440257"
---
# <a name="call-tree-view"></a>“调用关系树”视图
“调用关系树”视图显示在分析应用程序中遍历的函数执行路径。 树的根是应用程序或组件的入口点。 每个函数节点都列出它调用的所有函数以及有关这些函数调用的性能数据。

 “调用关系树”视图还可以展开以及突出显示消耗了最多时间或采样频率最高的函数的执行路径。 若要显示最损性能的路径，请右键单击函数，然后单击“展开热路径”。

 分析运行中的每个进程均显示为根节点。 可右键单击要设置为开始节点的节点，然后选择“设置根”，设置“调用树”视图的开始节点。

 设置根节点后，将从视图中排除所选节点的子树之外的所有其他条目。 可以将根节点重新设置为查看的节点。 在“调用树”视图窗口中，右键单击，然后选择“重新设置根”。

 可以自定义“调用树”视图来添加或删除列。 右键单击“列名称标题栏”，然后选择“添加/删除列”。

 通过限制显示的数据量，可配置“调用树”视图进行降噪。 通过使用降噪，性能问题在视图中就变得更为显著。 当性能问题易于区分时，分析就变得较为轻松了。 有关详细信息，请参阅[如何：在报表视图中配置降噪](../profiling/how-to-configure-noise-reduction-in-report-views.md)。

> [!NOTE]
> 如果将降噪配置为在启用时显示警告，则将在报告中显示信息栏。

 有关“调用树”视图中的列定义的详细信息，请参阅以下内容：

- [“调用树”视图](../profiling/call-tree-view-sampling-data.md)

- [“调用树”视图](../profiling/call-tree-view-instrumentation-data.md)

- [“调用树”视图 - 采样](../profiling/call-tree-view-dotnet-memory-sampling-data.md)

- [“调用树”视图](../profiling/call-tree-view-contention-data.md)

## <a name="see-also"></a>请参阅
- [性能报告视图](../profiling/performance-report-views.md)
- [了解检测数据值](../profiling/understanding-instrumentation-data-values.md)
- [了解采样数据值](../profiling/understanding-sampling-data-values.md)