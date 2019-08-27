---
title: 时间旅行调试实时 ASP.NET Azure 虚拟机
description: 了解如何记录和重播使用快照调试程序的 Azure 虚拟机上的实时 ASP.NET 应用。
ms.custom: ''
ms.date: 04/11/2019
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- aspnet
- azure
ms.openlocfilehash: 53dce8b6b468dd5754b5708afccdcbe6cb908d1d
ms.sourcegitcommit: ba5e072c9fedeff625a1332f22dcf3644d019f51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432214"
---
# <a name="record-and-replay-live-aspnet-apps-on-azure-virtual-machines-using-the-snapshot-debugger"></a>记录和重播使用快照调试程序的 Azure 虚拟机上的实时 ASP.NET 应用

Visual Studio Enterprise 中的时间旅行调试 (TTD) 预览版提供的功能来记录 Azure 虚拟机 (VM) 上运行的 Web 应用准确地重新构造并重播的执行路径。 TTD 与快照调试程序集成，并允许您后退并重播每行代码所需，从而帮助你隔离并识别问题可能只发生在生产环境中的任意次数。

捕获 TTD 录制将不会暂停应用程序。 但是，TDD 录制将添加到你正在运行的进程，降低它的速度基础上包括的大小和活动线程数的因素的很大的开销。

此功能处于预览版的发行版的 Visual Studio 2019 转实时许可证。

在本教程中，你将：

> [!div class="checklist"]
> * 启用时间旅行调试启动 Snapshot Debugger
> * 设置吸附点，并且收集一次移动录制
> * 开始调试时间旅行录制

## <a name="prerequisites"></a>系统必备

* 时间旅行调试的 Azure 虚拟机 (VM) 是仅适用于 Visual Studio 2019 Enterprise 或更高版本与**Azure 开发工作负荷**。 （可在“各个组件”选项卡的“调试和测试” > “Snapshot Debugger”下找到它    。）

    如果尚未安装，安装[Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/vs/)。

* 时间旅行调试是适用于以下的 Azure VM web 应用：
  * 运行 ASP.NET 应用程序 (AMD64) 上.NET Framework 4.8 或更高版本。

## <a name="start-the-snapshot-debugger-with-time-travel-debugging-enabled"></a>启用时间旅行调试启动 Snapshot Debugger

1. 打开该项目为你想要收集一次的旅行录制。

    > [!IMPORTANT]
    > 若要启动 TTD，您需要打开*相同版本的源代码*，它发布到 Azure VM 服务。

1. 选择“调试”>“附加 Snapshot Debugger...”  。选择你的 web 应用部署到 Azure VM 和 Azure 存储帐户。 选择**启用时间旅行调试**预览选项，然后单击**附加**。

      ![选择 Azure 资源](../debugger/media/time-travel-debugging-select-azure-resource-vm.png)

    > [!IMPORTANT]
    > 第一次为 VM 选择“附加 Snapshot Debugger”  时，IIS 将自动重启。

    元数据**模块**最初未激活。 导航到 web 应用和**开始收集**然后按钮将变为活动状态。 Visual Studio 现在处于快照调试模式下。

   ![快照调试模式](../debugger/media/snapshot-message.png)

    > [!NOTE]
    > Application Insights 站点扩展还支持快照调试。 如果遇到“站点扩展过期”错误消息，请参阅[快照调试的疑难解答提示和已知问题](../debugger/debug-live-azure-apps-troubleshooting.md)以获取升级详细信息。

   **模块**窗口中显示的所有模块的 Azure vm 的都加载时 (选择**调试 > Windows > 模块**要打开此窗口)。

   ![选中“模块”窗口](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint-and-collect-a-time-travel-recording"></a>设置吸附点，并且收集一次移动录制

1. 在代码编辑器中，单击你感兴趣设置吸附点的方法中的左滚动条槽。 请确保它是你已知将执行的代码。

   ![设置快照点](../debugger/media/time-travel-debugging-set-snappoint-settings.png)

1. 右键单击吸附点图标 （空心球），然后选择**操作**。 在中**快照设置**窗口中，单击**操作**复选框。 然后单击**到此方法的末尾收集时间旅行跟踪**复选框。

   ![收集一次传输到在方法结束跟踪](../debugger/media/time-travel-debugging-set-snappoint-action.png)

1. 单击“开始收集”以打开快照点  。

   ![开启快照点](../debugger/media/snapshot-start-collection.png)

## <a name="take-a-snapshot"></a>获取快照

吸附点启用，则它会捕获快照，只要的吸附点放置的位置的代码行执行。 此执行可能引起您的服务器上的实际请求。 若要强制命中快照点，请转到网站的浏览器视图，并执行命中快照点所需的任何操作。

## <a name="start-debugging-a-time-travel-recording"></a>开始调试时间旅行录制

1. 命中快照点时，快照将出现在诊断工具窗口。 若要打开此窗口，请依次选择“调试”>“窗口”>“显示诊断工具”  。

   ![打开快照点](../debugger/media/snapshot-diagsession-window.png)

1. 单击查看快照链接以打开录制在代码编辑器中按时间顺序查看。
  
   您可以执行的每一行代码使用记录的 TTD**继续**并**反向继续**按钮。 此外，**调试**工具栏可用于**显示下一条语句**，**单步执行**，**单步跳过**，**单步跳出**，**步骤回**，**逐过程执行回**，**步骤回**。

   ![开始调试](../debugger/media/time-travel-debugging-step-commands.png)

   此外可以使用**局部变量**，**监视**，和**调用堆栈**windows，并计算表达式。

   ![检查快照数据](../debugger/media/time-travel-debugging-start-debugging.png)

    网站本身仍然为实时事件和最终用户不受影响的任何后续 TTD 活动。 默认情况下，每个快照点只捕获一个快照：快照点在捕获快照后即关闭。 如果要在此快照点再捕获一个快照，可以通过单击“更新集合”来重新打开快照点  。

**需要帮助？** 请参阅[疑难解答和已知问题](../debugger/debug-live-azure-apps-troubleshooting.md)和[快照调试常见问题解答](../debugger/debug-live-azure-apps-faq.md)页。

## <a name="set-a-conditional-snappoint"></a>设置条件性快照点

如果难以在应用中重新创建某一特定状态，请考虑使用条件性快照点是否会有所帮助。 条件的吸附点帮助避免收集一次传输录制直到应用程序进入所需的状态，例如当一个变量具有你想要检查的特定值。 [可以设置使用表达式，筛选器条件或命中次数](../debugger/debug-live-azure-apps-troubleshooting.md)。

## <a name="next-steps"></a>后续步骤

在本教程中，已学习了如何收集记录适用于 Azure 虚拟机按时间顺序查看。 您可能想要详细了解快照调试程序。

> [!div class="nextstepaction"]
> [快照调试常见问题解答](../debugger/debug-live-azure-apps-faq.md)