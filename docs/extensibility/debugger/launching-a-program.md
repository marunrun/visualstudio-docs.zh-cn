---
title: 启动程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- programs, launching
ms.assetid: 6857e9c6-e44a-468a-afa4-f7c4a0b77844
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d9488c002e78828471374b954550843e16ff0e6b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344085"
---
# <a name="launch-a-program"></a>启动程序
想要调试的程序的用户可以按**F5**从 IDE 运行调试器。 这会开始一系列事件最终导致 IDE 的连接到调试引擎 (DE)，后者又连接，或附加，到该程序，如下所示：

1. IDE 首先调用项目包以获取解决方案的活动项目调试设置。 设置包括的开始目录、 环境变量，该程序将在其中运行的端口和 DE 要用于创建该程序，如果指定。 这些设置将传递给调试包。

2. 如果指定了德国，DE 调用操作系统来启动程序。 启动程序，因此加载程序的运行时环境。 例如，如果程序在 MSIL 中编写的将调用公共语言运行时来运行程序。

    或

    如果未指定 DE，端口将调用要启动程序，这会导致程序的运行时环境，若要加载的操作系统。

   > [!NOTE]
   > 如果部署用于启动某个程序，则很可能相同 DE 将被附加到该程序。

3. 具体取决于是否 DE 或端口启动程序，DE 或运行时环境的程序说明或节点，然后创建通知程序正在运行的端口。

   > [!NOTE]
   > 建议在运行时环境创建的程序节点中，因为程序节点是可调试的程序的轻量表示形式。 没有无需加载整个 DE 只是为了创建和注册程序节点。 如果设计 DE 运行 IDE，但没有 IDE 的过程中实际上正在运行，需要有一个组件，它可以将程序节点添加到该端口。

   新创建的程序，以及任何其他程序相关的或不相关的、 启动或附加到相同的 IDE，从编写调试会话。

   以编程方式，当用户首次按下**F5**，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的调试的包调用项目包 （这与正在启动程序的类型是关联） 通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A>反过来填充 out 方法<xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2>结构与解决方案的活动项目调试设置。 此结构通过调用传递回调试包<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A>方法。 调试包然后实例化启动要调试和任何关联的调试引擎的程序的会话调试管理器 (SDM)。

   传递给 SDM 的参数之一是 DE 要用来启动程序的 GUID。

   如果不是 DE GUID `GUID_NULL`，SDM 共同创建 DE，，然后调用其[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)方法来启动程序。 例如，如果程序用本机代码编写`IDebugEngineLaunch2::LaunchSuspended`可能会调用`CreateProcess`和`ResumeThread`（Win32 函数） 以运行该程序。

   启动程序，因此加载程序的运行时环境。 然后创建 DE 或运行时环境[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口来描述该程序，并将传递到此接口[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)以通知程序的端口正在运行。

   如果`GUID_NULL`传递，则该端口启动的程序。 程序开始运行后，创建运行时环境`IDebugProgramNode2`接口来描述该程序，并将其传递给`IDebugPortNotify2::AddProgramNode`。 这会通知程序正在运行的端口。 然后 SDM 将附加到正在运行的程序的调试引擎。

## <a name="in-this-section"></a>本节内容
 [通知端口](../../extensibility/debugger/notifying-the-port.md)介绍启动程序并通知该端口后，会发生什么情况。

 [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md)文档时调试会话已准备好将 DE 附加到该程序。

## <a name="related-sections"></a>相关章节
 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务，如启动程序和计算表达式。