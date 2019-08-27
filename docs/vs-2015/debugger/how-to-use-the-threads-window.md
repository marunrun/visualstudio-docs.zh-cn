---
title: 如何：使用线程窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.threads
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- Thread.Name property
- debugger, Threads window
- SetThreadName function
- Threads window
- '@TIB'
- debugging [Visual Studio], threads
ms.assetid: adfbe002-3d7b-42a9-b42a-5ac0903dfc25
caps.latest.revision: 48
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: da41524fcb231ea399dbbd2a2904afd935e5c4f8
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824238"
---
# <a name="how-to-use-the-threads-window"></a>如何：使用“线程”窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在中**线程**窗口中，您可以检查和使用的线程正在调试的应用程序中。  
  
 **线程**窗口包含其中每个行表示在应用程序中的线程的表。 默认情况下，该表列出应用程序中的所有线程，但您可以筛选列表以仅显示您感兴趣的线程。 每列都包含不同类型的信息。 您还可以隐藏某些列。 如果显示所有列，将从左到右显示以下信息：  
  
- 标志列，您可以在此处标记要格外关注的线程。 有关如何标记一个线程的信息，请参阅[如何：标记线程和取消标记线程](../debugger/how-to-flag-and-unflag-threads.md)。  
  
- 活动线程列，此处黄色箭头指示一个活动线程。 箭头的轮廓指示执行在调试器中分解的线程。  
  
- **ID**列，其中包含每个线程的标识号。  
  
- **托管 ID**列，包含托管线程的托管的标识号。  
  
- **类别**列中，将线程划分为用户界面线程、 远程过程调用处理程序或工作线程。 一个特殊类别标识应用程序的主线程。  
  
- **名称**列中，如果有的话，或按名称标识每个线程的\<无名称 >。  
  
- **位置**列，显示线程运行的位置。 可以展开此位置以显示线程的完整调用堆栈。  
  
- **优先级**列，包含系统已分配给每个线程的优先级。  
  
- **Affinity Mask**是高级的列，通常隐藏的列。 此列显示每个线程的处理器关联掩码。 在多处理器系统中，关联掩码确定线程可以在哪些处理器上运行。  
  
- **挂起项计数**列，包含挂起项计数。 此计数确定线程是否可以运行。 有关挂起项计数的解释，请参见本主题后面的“冻结和解冻线程”。  
  
- **进程名称**列，其中包含每个线程所属的进程。 在调试多个进程时，此列会很有用，但此列通常隐藏。  
  
### <a name="to-display-the-threads-window-in-break-mode-or-run-mode"></a>以中断模式或运行模式显示“线程”窗口  
  
- 上**调试**菜单，依次指向**Windows**，然后单击**线程**。  
  
### <a name="to-display-or-hide-a-column"></a>显示或隐藏列  
  
- 在顶部的工具栏**线程**窗口中，单击**列**，然后选中或清除要显示或隐藏的列的名称。  
  
### <a name="to-switch-the-active-thread"></a>切换活动线程  
  
- 任意执行以下步骤之一：  
  
  - 双击任一线程。  

  - 右键单击某个线程，然后单击**切换到线程**。  

    黄色箭头会出现在新活动线程的旁边。 箭头的灰色轮廓标识执行在调试器中分解的线程。  
  
## <a name="grouping-and-sorting-threads"></a>分组和排序线程  
 分组线程时，表中将显示每组的标题。 标题包含组的说明（如“辅助线程”或“未标记的线程”）和树控件。 每组的成员线程显示在组标题下。 如果要隐藏组的成员线程，可以使用树控件折叠组。  
  
 因为分组优先于排序，所以您可以先按类别（以此为例）分组线程，再按每个类别中的 ID 对其进行排序。  
  
#### <a name="to-sort-threads"></a>排序线程  
  
1. 在顶部的工具栏**线程**窗口中，单击任意列顶部的按钮。  
  
     线程现在按该列中的值进行排序。  
  
2. 如果希望颠倒排序顺序，请再次单击相同按钮。  
  
     在列表顶部显示的线程现在显示在底部。  
  
#### <a name="to-group-threads"></a>分组线程  
  
- 在中**线程**窗口工具栏上，单击**分组依据**列表，然后单击要分组线程所依据的条件。  
  
#### <a name="to-sort-threads-within-groups"></a>对组内线程排序  
  
1. 在顶部的工具栏**线程**窗口中，单击**分组依据**列表，然后单击要分组线程所依据的条件。  
  
2. 在中**线程**窗口中，单击任意列顶部的按钮。  
  
     线程现在按该列中的值进行排序。  
  
#### <a name="to-expand-or-collapse-all-groups"></a>展开或折叠所有组  
  
- 在顶部的工具栏**线程**窗口中，单击**展开组**或**折叠组**。  
  
## <a name="searching-for-specific-threads"></a>搜索特定线程  
 在 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 中，可以搜索与指定字符串匹配的线程。 搜索中的线程时**线程**窗口，窗口将显示在任何列中的搜索字符串匹配的所有线程。 信息包括在调用堆栈的顶部显示的线程位置**位置**列。 但是，默认情况下不搜索整个调用堆栈。  
  
#### <a name="to-search-for-specific-threads"></a>搜索特定线程  
  
- 在“线程”窗口顶部的工具栏中，转到“搜索”框，执行下列操作之一   ：  
  
  - 键入搜索字符串然后按 Enter。  

    \- 或 -  

  - 单击下拉列表旁边**搜索**框并选择上一次搜索的搜索字符串。  
  
- （可选）若要在搜索中包括整个调用堆栈，请选择“搜索调用堆栈”  。  
  
## <a name="freezing-and-thawing-threads"></a>冻结和解冻线程  
 当冻结线程时，即便资源可用，系统也不会开始执行该线程。  
  
 在本机代码中，您可以挂起或继续线程通过调用 Windows 函数`SuspendThread`并`ResumeThread`或者 MFC 函数[CWinThread::SuspendThread](https://msdn.microsoft.com/library/57189c7e-fd71-42e5-bc4b-3de7cd373d28)和[cwinthread:: Resumethread](https://msdn.microsoft.com/library/d6f97a2f-5c9f-4ee1-b978-d74938784db5). 如果您调用`SuspendThread`或`ResumeThread`，则更改*挂起项计数*，显示在**线程**窗口。 但是，如果冻结或解冻本机线程，则不会更改挂起项计数。 在本机代码中线程将无法执行，除非该线程解冻并且其挂起项计数为零。  
  
 在托管代码中，冻结或解冻线程不会更改挂起项计数。 在托管代码中，冻结线程的挂起项计数为 1。 在本机代码中，冻结线程的挂起项计数为 0，除非该线程由 `SuspendThread` 调用挂起。  
  
> [!NOTE]
> 在调试本机代码对托管代码的调用时，托管代码与调用它的本机代码在同一个物理线程中运行。 挂起或冻结本机线程也会冻结托管代码。  
  
#### <a name="to-freeze-or-thaw-execution-of-a-thread"></a>冻结或解冻线程的执行  
  
- 在顶部的工具栏**线程**窗口中，单击**冻结线程**或**解冻线程**。  
  
     此操作仅影响在“线程”窗口中选中的线程  。  
  
## <a name="displaying-flagged-threads"></a>显示标记的线程  
 在“线程”窗口中，可以用图标标记来标记要格外关注的线程  。 有关详细信息，请参阅[如何：标记线程和取消标记线程](../debugger/how-to-flag-and-unflag-threads.md)。 在“线程”窗口中，您可以选择显示所有线程或仅显示标记的线程。  
  
#### <a name="to-display-only-flagged-threads"></a>仅显示标记的线程  
  
- 选择标记按钮的左上角**线程**窗口。  
  
## <a name="displaying-thread-call-stacks-and-switching-between-frames"></a>显示线程调用堆栈并在帧之间切换  
 在多线程程序中，每个线程都有自己的调用堆栈。 “线程”窗口提供了一种查看这些堆栈的简便方法  。  
  
#### <a name="to-view-the-call-stack-of-a-thread"></a>查看线程的调用堆栈  
  
- 在中**位置**列中，单击线程位置旁边的倒的三角形。  
  
     此位置将展开以显示线程的调用堆栈。  
  
#### <a name="to-view-or-collapse-the-call-stacks-of-all-threads"></a>查看或折叠所有线程的调用堆栈  
  
- 在顶部的工具栏**线程**窗口中，单击**展开调用堆栈**或**折叠调用堆栈**。  
  
## <a name="see-also"></a>请参阅  
 [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [演练：调试多线程应用程序](../debugger/walkthrough-debugging-a-multithreaded-application.md)
