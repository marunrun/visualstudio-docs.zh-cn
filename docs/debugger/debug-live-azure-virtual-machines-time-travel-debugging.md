---
title: “按时间顺序查看调试”实时 ASP.NET Azure 虚拟机
description: 了解如何使用 Snapshot Debugger 在 Azure 虚拟机上记录和重播实时 ASP.NET 应用。
ms.custom: ''
ms.date: 04/11/2019
ms.topic: how-to
helpviewer_keywords:
- debugger
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- aspnet
- azure
ms.openlocfilehash: a44ecd7faeb3ec4cea7665678050580d7e4063a9
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350623"
---
# <a name="record-and-replay-live-aspnet-apps-on-azure-virtual-machines-using-the-snapshot-debugger"></a>使用 Snapshot Debugger 在 Azure 虚拟机上记录和重播实时 ASP.NET 应用

通过使用 Visual Studio Enterprise 中的“按时间顺序查看调试”(TTD) 预览功能，可以记录在 Azure 虚拟机 (VM) 上运行的 Web 应用，并能在其后准确地重新构建或重播执行路径。 TTD 与 Snapshot Debugger 集成，允许任意次数地后退并重播每一行代码，有助于隔离并识别只可能在生产环境中出现的问题。

捕获 TTD 记录时不会暂停应用程序。 但是，TDD 记录为正在运行的进程增加了很大的开销，会基于多项因素减慢进程的运行速度，这些因素包括进程大小和活动线程的数量。

此功能在带有上线许可证的 Visual Studio 2019 版本中提供预览。

在本教程中，你将：

> [!div class="checklist"]
> * 启动 Snapshot Debugger 并启用“按时间顺序查看调试”
> * 设置快照点并收集按时间顺序查看记录
> * 开始调试按时间顺序查看记录

## <a name="prerequisites"></a>先决条件

* 仅在具有 Azure 开发工作负载的 Visual Studio 2019 Enterprise 及更高版本中可以使用适用于 Azure 虚拟机 (VM) 的“按时间顺序查看调试”功能。 （可在“各个组件”选项卡的“调试和测试” > “Snapshot Debugger”下找到它  。）

    如果尚未安装，请安装 [Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/vs/)。

* “按时间顺序查看调试”适用于以下 Azure VM Web 应用：
  * 在 .NET Framework 4.8 或更高版本上运行的 ASP.NET 应用程序 (AMD64)。

## <a name="start-the-snapshot-debugger-with-time-travel-debugging-enabled"></a>启动 Snapshot Debugger 并启用“按时间顺序查看调试”

1. 打开要为其收集按时间顺序查看记录的项目。

    > [!IMPORTANT]
    > 若要开启 TTD，需要打开与已发布到 Azure VM 服务的版本相同版本的源代码。

1. 选择“调试”>“附加 Snapshot Debugger...”。选择 Web 应用部署到的 Azure VM 以及一个 Azure 存储帐户。 选择“启用‘按时间顺序查看调试’”预览选项，然后单击“附加” 。

      ![选择 Azure 资源](../debugger/media/time-travel-debugging-select-azure-resource-vm.png)

    > [!IMPORTANT]
    > 第一次为 VM 选择“附加 Snapshot Debugger”时，IIS 将自动重启。

    “模块”的元数据最初没有激活。 请导航到 Web 应用并点击“开始收集”按钮以完成激活。 Visual Studio 现在处于快照调试模式下。

   ![快照调试模式](../debugger/media/snapshot-message.png)

    > [!NOTE]
    > Application Insights 站点扩展还支持快照调试。 如果遇到“站点扩展过期”错误消息，请参阅[快照调试的疑难解答提示和已知问题](../debugger/debug-live-azure-apps-troubleshooting.md)以获取升级详细信息。

   “模块”窗口显示 Azure VM 的所有模块的加载时间（依次选择“调试”>“窗口”>“模块”可打开此窗口） 。

   ![选中“模块”窗口](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint-and-collect-a-time-travel-recording"></a>设置快照点并收集按时间顺序查看记录

1. 在代码编辑器中，单击自己感兴趣的方法中的左装订线以设置快照点。 请确保它是你已知将执行的代码。

   ![设置快照点](../debugger/media/time-travel-debugging-set-snappoint-settings.png)

1. 右键单击快照点图标（空心球）并选择“操作”。 在“快照设置”窗口中勾选“操作”复选框 。 然后勾选“收集按时间顺序查看跟踪直到此方法结束”复选框。

   ![收集按时间顺序查看跟踪直到此方法结束](../debugger/media/time-travel-debugging-set-snappoint-action.png)

1. 单击“开始收集”以打开快照点。

   ![开启快照点](../debugger/media/snapshot-start-collection.png)

## <a name="take-a-snapshot"></a>获取快照

启用快照点后，它会在快照点所在的代码行执行时捕获快照。 此执行可能由服务器上的实际请求引起。 若要强制命中快照点，请转到网站的浏览器视图，并执行命中快照点所需的任何操作。

## <a name="start-debugging-a-time-travel-recording"></a>开始调试按时间顺序查看记录

1. 命中快照点时，快照将出现在诊断工具窗口。 若要打开此窗口，请依次选择“调试”>“窗口”>“显示诊断工具”。

   ![打开快照点](../debugger/media/snapshot-diagsession-window.png)

1. 单击“查看快照”链接以在代码编辑器中打开按时间顺序查看记录。
  
   通过 TTD，可以使用“继续”或“反向继续”按钮执行记录的每行代码 。 此外，“调试”工具栏可用于“显示下一语句”、“单步执行”、“单步跳过”、“单步跳出”、“向后单步执行”、“向后单步跳过”以及“向后单步跳出”       。

   ![开始调试](../debugger/media/time-travel-debugging-step-commands.png)

   还可以使用“局部变量”、“监视”和“调用堆栈”窗口以及计算表达式  。

   ![检查快照数据](../debugger/media/time-travel-debugging-start-debugging.png)

    网站本身仍然是实时的，最终用户不会受到任何后续 TTD 活动的影响。 默认情况下，每个快照点只捕获一个快照：快照点在捕获快照后即关闭。 如果要在此快照点再捕获一个快照，可以通过单击“更新集合”来重新打开快照点。

**需要帮助？** 请参阅[疑难解答和已知问题](../debugger/debug-live-azure-apps-troubleshooting.md)和[快照调试常见问题解答](../debugger/debug-live-azure-apps-faq.md)页。

## <a name="set-a-conditional-snappoint"></a>设置条件性快照点

如果难以在应用中重新创建某一特定状态，请考虑使用条件性快照点是否会有所帮助。 条件性快照点可帮助避免在应用进入所需状态（例如变量具有你想要检查的特定值）前收集按时间顺序查看记录。 [可以使用表达式、筛选器或命中次数设置表达式](../debugger/debug-live-azure-apps-troubleshooting.md)。

## <a name="next-steps"></a>后续步骤

本教程已介绍如何收集 Azure 虚拟机的按时间顺序查看记录。 你可能想要阅读有关 Snapshot Debugger 更多详细信息。

> [!div class="nextstepaction"]
> [快照调试常见问题解答](../debugger/debug-live-azure-apps-faq.md)