---
title: 快照调试程序的起始页
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905235"
---
# <a name="getting-started-with-the-snapshot-debugger"></a>快照调试程序入门

Visual Studio 快照调试器现在连接到你的服务，可以开始收集快照，以帮助进行调试。

若要使用快照调试程序，在代码中设置一些吸附点，单击按钮以开始收集快照，然后运行您的方案。 代码运行时在其中已设置吸附点，创建你的应用程序的快照。 通过在 Visual Studio 中的诊断工具窗口中单击它，然后打开快照。 就像它是本地的一样，现在可以从你的服务调试快照。 有关详细说明，往下读。

## <a name="collect-and-view-snapshots"></a>收集和查看快照

快照调试程序从应用程序收集快照。 快照的时间，就像某时刻您 appication 图片。 时间和位置以在代码中设置吸附点收集快照告知 Visual Studio。 吸附点，在您将需要确保获取你要调查的问题的快照的任何条件。

### <a name="set-a-snappoint"></a>设置快照点

1. 在代码编辑器中，单击你感兴趣设置吸附点的代码行旁边的左滚动条槽。 请确保它是您知道将运行的代码。

    ![在编辑器中设置吸附点](../media/snapshot-startpage-set-snappoint.png)

    紫色六边形将显示你单击左侧的位置。

2. 单击“开始收集”以打开快照点。

### <a name="open-a-snapshot"></a>打开的快照

1. 命中吸附点，请在右侧的诊断工具窗口中会出现一个快照。 如果该窗口未打开，您可以通过选择打开它**调试** > **Windows** > **显示诊断工具**。

    ![在诊断工具窗口中的快照](../media/snapshot-startpage-diagsession-window.png)

2. 双击该快照将其打开。

### <a name="inspect-snapshot-data"></a>检查快照数据

在此视图中，可通过将鼠标悬停在变量上来查看数据提示；使用“局部变量”、“监视”和“调用堆栈”窗口；以及计算表达式。

网站本身仍然是实时的，最终用户不会受到影响。 默认情况下，只有一个快照是针对每个吸附点捕获的。 即，捕获快照后，吸附点会关闭。 如果要在此快照点再捕获一个快照，可以通过单击“更新集合”来重新打开快照点。

### <a name="set-a-logpoint"></a>设置记录点

1. 右键单击吸附点图标 （紫色六边形），然后选择**设置**。

2. 在中**吸附点设置**窗口中，选择**操作**。

    ![吸附点条件](../media/snapshot-startpage-logpoint.png)

3. 在中**消息**字段中，输入想要记录的日志消息。 还可以将日志消息中的变量放在大括号中，从而计算它们的值。

    如果愿意**将发送到输出窗口**，命中记录点时，诊断工具窗口中将显示该消息。

    如果愿意**发送到应用程序日志**，任何位置，您可以看到消息从出现的消息`System.Diagnostics.Trace`(或`ILogger`.NET Core 中)，如 App Insights，命中记录点时。

## <a name="learn-more"></a>了解更多信息

可以在上找到有关快照调试程序的详细信息[文档页](../debug-live-azure-applications.md)。 详细了解如何设置条件以使其更轻松地发现 bug。

## <a name="dont-show-me-this-again"></a>不再显示此信息

若要连接 Snapshot Debugger 永远不会显示快照调试程序起始页，更改**显示会话启动此入门页**选项**工具** >  **选项** > **快照调试器**。

![快照调试器工具选项页](../media/snapshot-startpage-tools-options.png)
