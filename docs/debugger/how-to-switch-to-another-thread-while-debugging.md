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
ms.openlocfilehash: 11ad6280ad1213008bbb8ca8f6311ca34231d308
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72732447"
---
# <a name="how-to-switch-to-another-thread-while-debugging-in-visual-studio-c-visual-basic-c"></a>如何：在 Visual Studio 中进行调试时切换到另一个线程（C#、Visual Basic、C++）
在调试多线程应用程序时，可以使用若干方法中的任何一种，从正在处理的线程切换到另一个线程。

> [!NOTE]
> 如果要控制线程的执行顺序，则需要[冻结和解冻线程](../debugger/get-started-debugging-multithreaded-apps.md)。

当你在代码编辑器和不同的多线程调试窗口中检查线程时，黄色箭头表示当前线程。 带有卷尾的绿色箭头表示非当前线程具有当前调试器上下文。

### <a name="to-switch-to-any-thread-that-appears"></a>切换到所显示的任何线程

- 在“线程”  或“并行监视”  窗口中，双击线程。

### <a name="to-switch-to-a-thread-in-a-source-window"></a>切换至源窗口中的线程

- 在左滚动条槽中，右键单击线程标记图标 ![线程标记](../debugger/media/dbg-thread-marker.png "ThreadMarker")，指向“切换到”，然后单击要切换到的线程的名称  。 快捷菜单仅显示该特定位置的线程。

     如果未显示任何线程标记，请在“线程”窗口中单击右键，确保选中了“在源中显示线程”   。

### <a name="to-switch-to-a-thread-in-the-debug-location-toolbar"></a>切换到“调试位置”工具栏中的线程

1. 在“调试位置”工具栏上，单击“线程”列表   。

2. 在列表中，单击要切换到的线程。

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
