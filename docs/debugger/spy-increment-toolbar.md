---
title: Spy + + 工具栏 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Spy++ toolbar
ms.assetid: 949c18fb-bb25-42ed-9130-c4a47869f24d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4fa1dfe0917fece3c814678295c5abd6013b426b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729736"
---
# <a name="spy-toolbar"></a>Spy++ 工具栏
工具栏出现在 Spy + + 菜单栏的下方。 若要显示或隐藏工具栏，请在 "**视图**" 菜单上单击 "**工具栏**"。

 工具栏上提供了下列控件。

## <a name="uielement-list"></a>UIElement 列表

|Button|效果|
|------------|------------|
|![Spy&#43; &#43; Windows 按钮](../debugger/media/icon_spy--_windows.gif "Icon_Spy + + _Windows")|显示系统中窗口和控件的树视图。 有关详细信息，请参阅[Windows 视图](../debugger/windows-view.md)。|
|!["&#43; &#43;监视进程" 按钮](../debugger/media/icon_spy--_processes.gif "Icon_Spy + + _Processes")|显示系统中进程的树视图。 有关详细信息，请参阅[进程视图](../debugger/processes-view.md)。|
|!["&#43; &#43;监视线程" 按钮](../debugger/media/icon_spy--_threads.gif "Icon_Spy + + _Threads")|显示系统中线程的树状视图。 有关详细信息，请参阅 "[线程" 视图](../debugger/threads-view.md)。|
|![Spy&#43; &#43;消息按钮](../debugger/media/icon_spy--_messages.gif "Icon_Spy + + _Messages")|创建一个窗口以显示窗口消息，并打开 "**消息选项**" 对话框，以便您可以选择将显示其消息的窗口，还可以选择其他选项。 有关详细信息，请参阅[消息视图](../debugger/messages-view.md)。|
|!["&#43; &#43;监视启动日志" 按钮](../debugger/media/icon_spy--_startlog.gif "Icon_Spy + + _StartLog")|启动消息日志记录并显示消息流。 只有在 "**消息**" 窗口为活动窗口时，此控件才可用。 有关详细信息，请参阅[如何：启动和停止消息日志显示](../debugger/how-to-start-and-stop-the-message-log-display.md)。|
|![Spy&#43; &#43;停止日志按钮](../debugger/media/icon_spy--_stoplog.gif "Icon_Spy + + _StopLog")|停止消息日志记录和消息流的显示。 只有在 "**消息**" 窗口为活动窗口时，此控件才可用。 有关详细信息，请参阅[如何：启动和停止消息日志显示](../debugger/how-to-start-and-stop-the-message-log-display.md)。|
|!["&#43; &#43;监视日志选项" 按钮](../debugger/media/icon_spy--_logoptions.gif "Icon_Spy + + _LogOptions")|显示 "[消息选项](../debugger/message-options-dialog-box.md)" 对话框。 使用此对话框可以选择要查看的 windows 和消息类型。 只有在 "**消息**" 窗口为活动窗口时，此控件才可用。|
|![Spy&#43; &#43;清除日志按钮](../debugger/media/spy--_clearlog.gif "Spy + + _ClearLog")|清除 "活动**消息**" 窗口的内容。 只有在 "**消息**" 窗口为活动窗口时，此控件才可用。|
|![Spy&#43; &#43;查找窗口按钮](../debugger/media/icon_spy--_findwindow.gif "Icon_Spy + + _FindWindow")|打开 "[查找窗口](../debugger/find-window-dialog-box.md)" 对话框，通过该对话框可以设置窗口搜索条件并显示属性或消息。 有关详细信息，请参阅[如何：使用查找程序工具](../debugger/how-to-use-the-finder-tool.md)。|
|![Spy&#43; &#43; "查找第一个窗口" 按钮](../debugger/media/icon_spy--_window.gif "Icon_Spy + + _Window")|在当前视图中搜索匹配的窗口、进程、线程或消息。|
|![Spy&#43; &#43; "查找下一个窗口" 按钮](../debugger/media/icon_spy--_nextwindow.gif "Icon_Spy + + _NextWindow")|在当前视图中搜索下一个匹配窗口、进程、线程或消息。 仅当存在一个不唯一的有效搜索结果时，此控件（和相关菜单命令）才可用。 例如，当您在窗口树中使用窗口句柄作为搜索条件时，它将生成唯一的结果，因为只有一个窗口处于该句柄的窗口树中。在此实例中，"**找不到下一个**" 不可用。|
|![Spy&#43; &#43;查找上一个窗口按钮](../debugger/media/icon_spy--_prevwindow.gif "Icon_Spy + + _PrevWindow")|在当前视图中搜索上一个匹配窗口、进程、线程或消息。 仅当存在一个不唯一的有效搜索结果时，此控件（和相关菜单命令）才可用。 例如，当您在窗口树中使用窗口句柄作为搜索条件时，它将生成唯一的结果，因为只有一个窗口处于该句柄的窗口树中。在此实例中，"**找不到上一个**" 不可用。|
|![Spy&#43; &#43;属性资源管理器按钮](../debugger/media/icon_spy--_propexp.gif "Icon_Spy + + _PropExp")|显示在 "窗口" 视图中选择的窗口的属性。|
|![Spy&#43; &#43;刷新按钮](../debugger/media/icon_spy--_refresh.gif "Icon_Spy + + _Refresh")|刷新系统视图。|

## <a name="see-also"></a>请参阅
- [使用 Spy++](../debugger/using-spy-increment.md)
- [Spy++ 视图](../debugger/spy-increment-views.md)
- [Spy++ 参考](../debugger/spy-increment-reference.md)