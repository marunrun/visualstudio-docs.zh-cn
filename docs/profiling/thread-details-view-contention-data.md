---
title: “线程详细信息”视图 - 争用数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.threaddetails
helpviewer_keywords:
- Thread Details view
ms.assetid: 874c3b1c-88d8-479a-bb35-1291d9aa8e67
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 679fd9fd039fa903f5df5a479fa4f0e119bb7a9c
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778162"
---
# <a name="thread-details-view---contention-data"></a>“线程详细信息”视图 - 争用数据
“线程详细信息”视图显示在分析运行的所选线程中，针对资源的争用所导致的阻塞事件的时间线关系图。 如果由于另一个线程已锁定对资源的访问，因此线程被迫挂起执行，则会发生阻塞事件。

 此视图将线程的执行时间线表示为水平条，而将阻塞事件表示为线程水平时间线上的垂直条。 如有必要，可以放大时间线的每个部分以查看单个事件。 若要查看导致事件的函数的执行路径，请单击事件条。 函数会出现在“调用堆栈”  窗口中。 当函数的源代码可用时，可以单击该函数名，以便在 Visual Studio IDE 中编辑源文件。

## <a name="navigate-the-timeline"></a>导航时间线

#### <a name="to-zoom-in-on-a-timeline-segment"></a>放大时间线片段

- 单击鼠标指针并进行拖动以选择时间线的某个区域。

     释放鼠标后，视图会放大到所选时间片段。 可以重复该过程以放大显示更多详细信息。 时间滚动条上的滚动框表示显示在视图中的时间片段的相对大小。

#### <a name="to-zoom-out-on-a-timeline"></a>缩小时间线

- 单击“缩小”  以返回到以前的缩放级别。

- 单击“缩放重置”  以在视图中显示整个时间线。

#### <a name="to-view-the-call-stack-of-an-event"></a>查看事件的调用堆栈

- 在时间线关系图中，单击表示事件的垂直条。

#### <a name="to-view-or-edit-the-source-code-of-a-function-in-the-call-stack"></a>查看或编辑调用堆栈中的函数的源代码

- 在“调用堆栈”  窗口中，单击函数名。

  函数源代码必须是当前项目的一部分。

#### <a name="to-view-the-contention-events-of-a-resource-in-all-threads-in-the-profiling-run"></a>查看分析运行中所有线程中的每个资源的争用事件

- 在时间线关系图中，单击资源的名称或 ID。

     所选资源的[“资源详细信息”](../profiling/resource-details-view-contention-data.md)视图会出现。

#### <a name="to-view-the-thread-contention-data-in-the-processes-window"></a>在“进程”窗口中查看线程争用数据

- 在时间线关系图中，单击“总计”  。

     [“进程视图”](../profiling/process-view-contention-data.md)会出现，其中包含所选线程。
