---
title: 如何 - 在窗口视图中搜索窗口 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- windows, searching in Windows view
ms.assetid: 30306970-b861-4315-acf8-f86a43d4e73b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fb5fb871ebf03595c0baca0336e8449fe39029f3
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349232"
---
# <a name="how-to-search-for-a-window-in-windows-view"></a>如何：在窗口视图中搜索窗口
可以通过使用句柄、标题、类别或标题和类别的组合作为搜索条件，在窗口视图中搜索特定窗口。 还可以指定搜索的初始方向。 对话框中的字段将显示窗口树中所选窗口的属性。

 先从扩展到第二级（所有属于桌面子级的窗口）的树开始，以便通过类别名称和标题来标识桌面级窗口。 选择桌面级窗口后，就可以展开该级别以查找特定的子窗口。

### <a name="to-search-for-a-window-in-windows-view"></a>在窗口视图中搜索窗口

1. 排列窗口，以使 Spy++、[窗口视图](../debugger/windows-view.md)窗口和目标窗口可见。

2. 从“搜索”菜单中选择“查找窗口”。

    此时将打开[“窗口搜索”对话框](../debugger/window-search-dialog-box.md)。

   > [!TIP]
   > 若要减少屏幕干扰，请选择“隐藏 Spy”选项。 此选项会隐藏 Spy++ 主窗口，但“窗口搜索”对话框仍显示在其他应用程序的顶部。 单击“确定”或“取消”时，或清除“隐藏 Spy++”选项时，将还原 Spy++ 主窗口。

3. 将查找程序工具拖到目标窗口之上。 拖动该工具时，“窗口搜索”对话框会显示有关所选窗口的详细信息。

   - 或 -

     如果知道所需窗口的句柄（例如，来自调试器），则可以在“句柄”框中键入它。

   - 或 -

     如果知道所需窗口的标题和/或类别，则可以在“标题”和“类别”文本框中键入它们，并清除“句柄”文本框。

4. 选择“向上”或“向上”作为搜索的初始方向。

5. 单击 **“确定”** 。

    如果找到了匹配的窗口，它会在[窗口视图](../debugger/windows-view.md)窗口中突出显示。