---
title: 消息视图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.messagesview
helpviewer_keywords:
- Messages view
ms.assetid: 14c2a786-c23a-4b2d-acad-8c32a856c70d
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3765b9804224549c98b57cd1b0a44f0330d278b5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157489"
---
# <a name="messages-view"></a>消息视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

每个窗口都有相关联的消息流。 消息视图窗口会显示此消息流。 显示的窗口句柄、 消息代码和消息。 可以创建线程或进程以及消息视图。 这样，您可以查看发送到特定的进程或线程，尤其是用于捕获窗口初始化消息所拥有的所有窗口的消息。  
  
 一个典型的消息视图窗口，如下所示。 请注意，第一列包含窗口句柄，并且第二列包含消息代码 (中所述[消息代码](../debugger/message-codes.md))。 已解码的消息参数和返回值将位于右侧。  
  
 ![Spy&#43; &#43;消息视图](../debugger/media/spy-messagesview.png "Spy + + _MessagesView")  
Spy++ 消息视图  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-open-a-messages-view-for-a-window-process-or-thread"></a>若要打开的窗口、 进程或线程的消息视图  
  
1. 将焦点移至[Windows 视图](../debugger/windows-view.md)，[进程视图](../debugger/processes-view.md)，或[线程视图](../debugger/threads-view.md)窗口。  
  
2. 查找你想要检查，其消息的项的节点并选择它。  
  
3. 从**Spy**菜单中，选择**日志消息**。  
  
     [消息选项对话框](../debugger/message-options-dialog-box.md)随即打开。  
  
4. 选择你想要显示的消息的选项。  
  
5. 按**确定**开始日志记录消息。  
  
     一个视图窗口将打开，消息的以及**消息**菜单添加到 Spy + + 工具栏。 根据所选的选项，消息开始流式传送到活动的消息视图窗口。  
  
6. 在必须足够多的消息，请选择**停止日志记录**从**消息**菜单。  
  
## <a name="in-this-section"></a>本节内容  
 [控制消息视图](../debugger/how-to-control-messages-view.md)  
 说明如何管理消息视图。  
  
 [消息在消息视图中搜索](../debugger/how-to-search-for-a-message-in-messages-view.md)  
 介绍如何在消息视图中查找特定的消息。  
  
 [启动和停止显示消息日志](../debugger/how-to-start-and-stop-the-message-log-display.md)  
 介绍如何启动和停止消息日志记录。  
  
 [消息代码](../debugger/message-codes.md)  
 定义消息消息视图中列出的代码。  
  
 [显示消息属性](../debugger/how-to-display-message-properties.md)  
 如何显示一条消息的详细信息。  
  
## <a name="related-sections"></a>相关章节  
 [Spy++ 视图](../debugger/spy-increment-views.md)  
 介绍 windows、 消息、 进程和线程的 Spy + + 树的视图。  
  
 [使用 Spy++](../debugger/using-spy-increment.md)  
 介绍 Spy + + 工具，并说明如何使用它。  
  
 [“消息选项”对话框](../debugger/message-options-dialog-box.md)  
 用于选择要在活动的消息视图中列出的消息。  
  
 [“消息搜索”对话框](../debugger/message-search-dialog-box.md)  
 用于查找特定的消息在消息视图中的节点。  
  
 [“消息属性”对话框](../debugger/message-properties-dialog-box.md)  
 用于显示在消息视图中选择一条消息的属性。  
  
 [Spy++ 参考](../debugger/spy-increment-reference.md)  
 包含描述每个 Spy + + 菜单和对话框的章节。
