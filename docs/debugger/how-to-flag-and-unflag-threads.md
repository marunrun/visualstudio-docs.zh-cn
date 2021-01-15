---
title: 标记线程和取消标记线程 | Microsoft Docs
description: 了解如何在 Visual Studio 中标记线程或取消标记线程。 标记或取消标记单个线程、若干线程或所有线程。 仅标记你的代码或与模块关联的代码。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: e9b7ce5db863987d530fe9e68d026a94474fc13c
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98149490"
---
# <a name="how-to-flag-and-unflag-threads-c-visual-basic-c"></a>如何：标记线程和取消标记线程（C#、Visual Basic、C++）

在“线程”、“并行堆栈”（线程视图）、“并行监视”和“GPU 线程”窗口中，可以使用图标来标记要特别关注的线程   。 此图标有助于您和其他人将标记的线程与其他线程区别开来。

在“调试位置”工具栏上的“线程”列表以及其他多线程调试窗口中，标记的线程还得到特殊处理 。 可以在“线程”列表或其他窗口中显示全部线程或仅显示标记的线程。

### <a name="to-flag-or-unflag-a-thread"></a>标记或取消标记线程

- 在“线程”或“并行监视”窗口中，找到感兴趣的线程，单击标记图标选中或清除标记 。
- 在“并行堆栈”窗口中，右键单击线程或线程组，然后选择“标记/\<thread>”或“取消标记/\<thread>”  。

### <a name="to-unflag-all-threads"></a>取消标记所有线程

- 在“线程”窗口中右击任意线程，然后单击“取消标志所有线程” 。
- 在“并行监视”窗口中，选择所有标记的线程，然后右键单击并选择“取消标记” 。

### <a name="to-display-only-flagged-threads"></a>仅显示标记的线程

- 在其中一个多线程调试窗口中选择“仅显示标记的线程”按钮。

### <a name="to-flag-just-my-code"></a>标记“仅我的代码”

1. 在“线程”窗口顶部的工具栏中，单击标志图标。

2. 在下拉列表中，单击“标记‘仅我的代码’”。

### <a name="to-flag-threads-that-are-associated-with-selected-modules"></a>标记与选定模块关联的线程

1. 在“线程”窗口的工具栏中，单击标志图标。

2. 在下拉列表中，单击“标记自定义模块选择”。

3. 在“选择模块”对话框中，选择需要的模块。

4. （可选）在“搜索”框中，键入用于搜索特定模块的字符串。

5. 单击 **“确定”** 。

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [开始调试多线程应用程序](../debugger/get-started-debugging-multithreaded-apps.md)
- [演练：使用“线程”窗口调试多线程应用程序](../debugger/how-to-use-the-threads-window.md)