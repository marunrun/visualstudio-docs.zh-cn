---
title: 窗口视图 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.windowsview
helpviewer_keywords:
- Windows view
ms.assetid: 154786ce-c803-4bfb-8198-f7962a900363
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fef652cbaa83fde61f098fb8fcef9558473fe19a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900849"
---
# <a name="windows-view"></a>窗口视图
首次打开 Spy++ 时，窗口视图将显示系统中所有窗口和控件的树。 显示窗口句柄和类名称。 当前桌面窗口位于树的顶部。 所有其他窗口均为桌面的子级，并且根据标准窗口层次结构列出。 同级窗口显示在其父项下缩进的可扩展列表中。

 下图显示了一个典型的 Spy++ 窗口视图，其中顶级节点已展开。

 ![Spy&#43;&#43; 窗口视图](../debugger/media/spy--_windowsview.png "Spy++_WindowsView") Spy++ 窗口视图

 当前桌面窗口位于树的顶部。 所有其他窗口均为桌面的子级，并且根据标准窗口层次结构列出，同级窗口按 Z 顺序排序。 通过单击节点旁边的 + 或 - 符号，可以展开或折叠树的任何父节点。

 当窗口视图具有焦点时，可以使用[“窗口搜索”对话框](../debugger/window-search-dialog-box.md)中的“查找程序”工具显示系统中任何打开窗口的信息。

## <a name="in-this-section"></a>本节内容
 [如何：使用查找程序工具](../debugger/how-to-use-the-finder-tool.md) 介绍此工具如何扫描窗口中的属性或消息。

 [如何：在窗口视图中搜索窗口](../debugger/how-to-search-for-a-window-in-windows-view.md) 说明如何在窗口视图中查找特定窗口。

 [如何：显示窗口属性](../debugger/how-to-display-window-properties.md) 打开“窗口属性”对话框的过程。

## <a name="related-sections"></a>相关章节
 [Spy++ 视图](../debugger/spy-increment-views.md) 介绍窗口、消息、进程和线程的 Spy++ 树状视图。

 [使用 Spy++](../debugger/using-spy-increment.md) 介绍 Spy++ 工具，并说明其使用方式。

 [“查找窗口”对话框](../debugger/find-window-dialog-box.md) 用于查看特定窗口中的属性或消息。

 [“窗口搜索”对话框](../debugger/window-search-dialog-box.md) 用于在窗口视图中查找特定窗口的节点。

 [“窗口属性”对话框](../debugger/window-properties-dialog-box.md) 用于显示窗口视图中所选窗口的属性。

 [Spy++ 参考](../debugger/spy-increment-reference.md) 包括介绍每个 Spy++ 菜单和对话框的章节。