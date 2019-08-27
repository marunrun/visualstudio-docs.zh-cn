---
title: 在调试时切换到另一个线程
ms.custom: seodec18
ms.date: 04/27/2017
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threads, switching [debugging]
ms.assetid: 5cd76c52-76fa-4fcc-b37e-e9f0ecac0e9e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 31eb3427a441b4b79bbd57d9da9871118173b15c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62849410"
---
# <a name="how-to-switch-to-another-thread-while-debugging-in-visual-studio-c-visual-basic-c"></a>如何：在 Visual Studio 中调试时切换到另一个线程 (C#，Visual Basic 中， C++)
当调试多线程应用程序时，可以使用几种方法之一从你一直在处理到另一个线程的线程切换。

> [!NOTE]
> 如果你想要控制线程的执行的顺序，则需要[冻结和解冻线程](../debugger/get-started-debugging-multithreaded-apps.md)。

检查在代码编辑器和不同的多线程调试窗口中的线程时，黄色箭头指示当前线程。 带有卷尾的绿色箭头指示非当前线程具有当前的调试器上下文。

### <a name="to-switch-to-any-thread-that-appears"></a>若要切换到显示的任何线程

- 在中**线程**或**并行监视**窗口中，双击线程。

### <a name="to-switch-to-a-thread-in-a-source-window"></a>切换至源窗口中的线程

- 在左滚动条槽，右击线程标记图标![线程标记](../debugger/media/dbg-thread-marker.png "ThreadMarker")，指向**切换到**，然后单击你想要切换的线程的名称. 快捷菜单仅显示该特定位置的线程。

     如果没有线程标记就会显示，请右键单击在**线程**窗口，并验证**在源中显示线程**处于选中状态。

### <a name="to-switch-to-a-thread-in-the-debug-location-toolbar"></a>切换到“调试位置”工具栏中的线程

1. 上**调试位置**工具栏上，单击**线程**列表。

2. 在列表中，单击要切换到的线程。

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
