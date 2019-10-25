---
title: 如何：标记线程和取消标记线程 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- treads, switching [debugging]
ms.assetid: 952d579d-6911-413e-b3e5-54e7e797e70c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68a2ce8b6ec429b3f7f5cd782c3dac52602eff16
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733235"
---
# <a name="how-to-flag-and-unflag-threads-c-visual-basic-c"></a>如何：标记线程和取消标记线程C#（、Visual Basic C++、）

您可以通过使用 "**线程**"、"**并行堆栈**" （"线程" 视图）、"**并行监视**" 和 " **GPU 线程**" 窗口中的图标来标记要特别注意的线程。 此图标有助于您和其他人将标记的线程与其他线程区别开来。

标记线程还会在 "**调试位置**" 工具栏上的**线程**列表和其他多线程调试窗口中接收特殊处理。 您可以显示**线程**列表或其他窗口中的所有线程或仅显示标记的线程。

### <a name="to-flag-or-unflag-a-thread"></a>标记或取消标记线程

- 在 "**线程**" 或 "**并行监视**" 窗口中，找到感兴趣的线程，并单击标志图标以选择或清除标志。
- 在 "**并行堆栈**" 窗口中，右键单击线程或线程组，然后选择 "**标志/\<thread >** 或取消**标记/\<thread >** "。

### <a name="to-unflag-all-threads"></a>取消标记所有线程

- 在“线程”窗口中右击任意线程，然后单击“取消标志所有线程”。
- 在 "**并行监视**" 窗口中，选择所有标记的线程，然后右键单击并选择 "取消**标记**"。

### <a name="to-display-only-flagged-threads"></a>仅显示标记的线程

- 选择其中一个多线程调试窗口中的 "**仅显示标记的线程**" 按钮。

### <a name="to-flag-just-my-code"></a>标记“仅我的代码”

1. 在“线程”窗口顶部的工具栏中，单击标志图标。

2. 在下拉列表中，单击“标记‘仅我的代码’”。

### <a name="to-flag-threads-that-are-associated-with-selected-modules"></a>标记与选定模块关联的线程

1. 在“线程”窗口的工具栏中，单击标志图标。

2. 在下拉列表中，单击“标记自定义模块选择”。

3. 在“选择模块”对话框中，选择需要的模块。

4. （可选）在“搜索”框中，键入用于搜索特定模块的字符串。

5. 单击“确定”。

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)
- [演练：使用 "线程" 窗口调试多线程应用程序](../debugger/how-to-use-the-threads-window.md)