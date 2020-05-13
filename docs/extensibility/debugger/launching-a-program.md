---
title: 启动计划 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- programs, launching
ms.assetid: 6857e9c6-e44a-468a-afa4-f7c4a0b77844
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf638e0c96c7df1de2650260427a972a07efce23
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738477"
---
# <a name="launch-a-program"></a>启动程序
想要调试程序的用户可以按**F5**从 IDE 运行调试器。 这将启动一系列事件，最终导致 IDE 连接到调试引擎 （DE），调试引擎又连接到程序，如下所示：

1. IDE 首先调用项目包以获取解决方案的活动项目调试设置。 这些设置包括起始目录、环境变量、程序将在其中运行的端口以及用于创建程序的 DE（如果指定）。 这些设置将传递到调试包。

2. 如果指定了 DE，DE 将调用操作系统来启动程序。 启动程序后，程序的运行时环境将加载。 例如，如果程序是在 MSIL 中编写的，则将调用通用语言运行时来运行该程序。

    \- 或 -

    如果未指定 DE，端口将调用操作系统启动程序，这将导致加载程序的运行时环境。

   > [!NOTE]
   > 如果 DE 用于启动程序，则同一 DE 很可能将附加到该程序。

3. 根据 DE 还是端口启动程序，DE 或运行时环境然后创建程序说明或节点，并通知端口程序正在运行。

   > [!NOTE]
   > 建议运行时环境创建程序节点，因为程序节点是可调试的程序的轻量级表示形式。 无需仅加载整个 DE 来创建和注册程序节点。 如果 DE 设计为在 IDE 过程中运行，但实际没有 IDE 运行，则需要有一个组件可以将程序节点添加到端口。

   新创建的程序以及从同一 IDE 启动或附加到的任何其他程序（相关或不相关程序）组成调试会话。

   在编程上，当用户首次按**F5**时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，调试包通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A>方法调用项目包（与正在启动的程序类型相关联），该方法又使用解决方案的活动项目调试设置填充<xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2>结构。 此结构通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A>方法传回调试包。 然后，调试包实例化会话调试管理器 （SDM），该管理器启动正在调试的程序和任何关联的调试引擎。

   传递给 SDM 的参数之一是用于启动程序的 DE 的 GUID。

   如果 DE GUID`GUID_NULL`不是 ，则 SDM 共同创建 DE，然后调用其[Launch暂停](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)方法启动程序。 例如，如果程序是用本机代码编写的，`IDebugEngineLaunch2::LaunchSuspended`则可能会调用`CreateProcess`和`ResumeThread`（Win32 函数）来运行该程序。

   启动程序后，将加载程序的运行时环境。 然后，DE 或运行时环境创建一个[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口来描述程序，并将此接口传递给[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)以通知端口程序正在运行。

   如果`GUID_NULL`传递，则端口将启动该程序。 程序运行后，运行时环境将创建一个`IDebugProgramNode2`接口来描述程序并将其传递给`IDebugPortNotify2::AddProgramNode`。 这将通知端口程序正在运行。 然后 SDM 将调试引擎附加到正在运行的程序。

## <a name="in-this-section"></a>在本节中
 [通知端口](../../extensibility/debugger/notifying-the-port.md)说明程序启动后会发生什么情况，并通知端口。

 [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md)当调试会话准备好将 DE 附加到程序时，将记录。

## <a name="related-sections"></a>相关章节
 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务的链接，例如启动程序和评估表达式。
