---
title: Snapshot Debugger 的起始页
ms.date: 07/14/2018
robots: noindex, nofollow
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cf2aba33089623dc98a90c23166291bb2d6e7123
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905235"
---
# <a name="getting-started-with-the-snapshot-debugger"></a>Snapshot Debugger 入门

Visual Studio Snapshot Debugger 现在已连接到你的服务，你可以开始收集快照以帮助进行调试。

若要使用 Snapshot Debugger，请在代码中设置一些吸附点，单击按钮以开始收集快照，然后运行方案。 当其中设置了快照点的代码运行时，将拍摄应用程序的快照。 然后，通过在 Visual Studio 的“诊断工具”窗口中单击快照来打开它。 现在可以从服务调试快照，如同它在本地一样。 有关详细说明，请继续阅读。

## <a name="collect-and-view-snapshots"></a>收集和查看快照

Snapshot Debugger 会从应用程序收集快照。 快照类似于应用程序在某个时间点的概况。 通过在代码中设置快照点，可告知 Visual Studio 在何时和何处收集快照。 在快照点中，可以设置所有需要的条件，以确保获取所调查的问题的快照。

### <a name="set-a-snappoint"></a>设置快照点

1. 在代码编辑器中，单击你感兴趣的代码行旁边的左滚动条槽以设置快照点。 请确保它是你已知将运行的代码。

    ![在编辑器中设置快照点](../media/snapshot-startpage-set-snappoint.png)

    在左侧单击的位置处将出现紫色六边形。

2. 单击“开始收集”以打开快照点。

### <a name="open-a-snapshot"></a>打开快照

1. 命中快照点时，快照将出现在右侧的诊断工具窗口。 如果该窗口未打开，则可以通过选择“调试” > “窗口” > “显示诊断工具”来打开它。

    ![诊断工具窗口中的快照](../media/snapshot-startpage-diagsession-window.png)

2. 双击快照以将其打开。

### <a name="inspect-snapshot-data"></a>检查快照数据

在此视图中，可通过将鼠标悬停在变量上来查看数据提示；使用“局部变量”、“监视”和“调用堆栈”窗口；以及计算表达式。

网站本身仍然是实时的，最终用户不会受到影响。 默认情况下，每个快照点只捕获一个快照。 也就是说，在捕获快照之后，快照点将关闭。 如果要在此快照点再捕获一个快照，可以通过单击“更新集合”来重新打开快照点。

### <a name="set-a-logpoint"></a>设置记录点

1. 右键单击快照点图标（紫色六边形），然后选择“设置”。

2. 在“快照点设置”窗口中，选择“操作” 。

    ![快照点条件](../media/snapshot-startpage-logpoint.png)

3. 在“消息”字段中，输入要记录的日志消息。 还可以将日志消息中的变量放在大括号中，从而计算它们的值。

    如果选择“发送到输出窗口”，则在点击记录点时，消息将出现在“诊断工具”窗口中。

    如果选择“发送到应用程序日志”，则在点击记录点时，消息会出现在可以看到来自 `System.Diagnostics.Trace`（或 .NET Core 中的 `ILogger`）的消息的任何位置，例如 App Insights。

## <a name="learn-more"></a>了解更多信息

可以在[文档页面](../debug-live-azure-applications.md)中找到有关 Snapshot Debugger 的详细信息。 详细了解如何设置条件，以更轻松地找到 bug。

## <a name="dont-show-me-this-again"></a>不再显示此信息

若要在连接 Snapshot Debugger 时不再显示 Snapshot Debugger 起始页，请在“工具” > “选项” > “Snapshot Debugger”中更改“在会话开始时显示‘入门’页面”选项。

![Snapshot Debugger 工具选项页](../media/snapshot-startpage-tools-options.png)
