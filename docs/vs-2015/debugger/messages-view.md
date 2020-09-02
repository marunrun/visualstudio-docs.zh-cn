---
title: 消息视图 | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157489"
---
# <a name="messages-view"></a>消息视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

每个窗口都有一个关联的消息流。 消息视图窗口显示此消息流。 窗口句柄、消息代码和消息会进行显示。 也可以为线程或进程创建消息视图。 这使你可以查看发送到特定进程或线程所拥有的所有窗口的消息，这对于捕获窗口初始化消息特别有用。  
  
 下面显示了典型的消息视图窗口。 请注意，第一列包含窗口句柄，第二列包含消息代码（在[消息代码](../debugger/message-codes.md)中进行了说明）。 解码的消息参数和返回值位于右侧。  
  
 ![Spy&#43;&#43; 消息视图](../debugger/media/spy-messagesview.png "Spy + + _MessagesView")  
Spy++ 消息视图  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-open-a-messages-view-for-a-window-process-or-thread"></a>为窗口、进程或线程打开消息视图  
  
1. 将焦点移动到[窗口视图](../debugger/windows-view.md)、[进程视图](../debugger/processes-view.md)或[线程视图](../debugger/threads-view.md)窗口上。  
  
2. 查找要检查其消息的项的节点，然后选择它。  
  
3. 从“Spy”菜单中，选择“日志消息” 。  
  
     [“消息选项”对话框](../debugger/message-options-dialog-box.md)会打开。  
  
4. 为要显示的消息选择选项。  
  
5. 按“确定”以开始记录消息。  
  
     消息视图窗口会打开，并且“消息”菜单会添加到 Spy++ 工具栏。 根据所选的选项，消息开始流入活动消息视图窗口中。  
  
6. 有足够消息时，从“消息”菜单中选择“停止记录”。  
  
## <a name="in-this-section"></a>本节内容  
 [控制消息视图](../debugger/how-to-control-messages-view.md)  
 说明如何管理消息视图。  
  
 [在 "消息" 视图中搜索消息](../debugger/how-to-search-for-a-message-in-messages-view.md)  
 说明如何在 "消息" 视图中查找特定消息。  
  
 [启动和停止消息日志显示](../debugger/how-to-start-and-stop-the-message-log-display.md)  
 说明如何启动和停止消息日志记录。  
  
 [消息代码](../debugger/message-codes.md)  
 为 "消息" 视图中列出的消息定义代码。  
  
 [显示消息属性](../debugger/how-to-display-message-properties.md)  
 如何显示消息的详细信息。  
  
## <a name="related-sections"></a>相关章节  
 [Spy++ 视图](../debugger/spy-increment-views.md)  
 说明窗口的 Spy + + 树视图、消息、进程和线程。  
  
 [使用 Spy++](../debugger/using-spy-increment.md)  
 介绍 Spy + + 工具，并说明如何使用它。  
  
 [“消息选项”对话框](../debugger/message-options-dialog-box.md)  
 用于选择在 "活动消息" 视图中列出的消息。  
  
 [“消息搜索”对话框](../debugger/message-search-dialog-box.md)  
 用于在 "消息" 视图中查找特定消息的节点。  
  
 [“消息属性”对话框](../debugger/message-properties-dialog-box.md)  
 用于显示在消息视图中选择的消息的属性。  
  
 [Spy++ 参考](../debugger/spy-increment-reference.md)  
 包括介绍每个 Spy + + 菜单和对话框的部分。
