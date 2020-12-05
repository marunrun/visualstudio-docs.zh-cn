---
title: 启动程序 |Microsoft Docs
description: 了解在使用 F5 从 IDE 中运行调试器时，调试程序时所发生的一系列事件。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 0dce13e49eeadf4dc02fec07707bebcfe164ed9c
ms.sourcegitcommit: 42981ace63c0f2b087de5703ca76b8dcdd93a719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "96606692"
---
# <a name="launch-a-program"></a>启动程序
要调试程序的用户可以按 **F5** 从 IDE 中运行调试器。 这将开始一系列事件，这些事件最终会导致 IDE 连接到调试引擎， (DE) ，然后将其连接或附加到程序，如下所示：

1. IDE 首先调用项目包以获取解决方案的活动项目调试设置。 这些设置包括起始目录、环境变量、程序将在其中运行的端口以及用于创建程序的 DE （如果已指定）。 这些设置将传递给调试包。

2. 如果指定了 DE，则 DE 会调用操作系统来启动程序。 作为启动程序的结果，程序的运行时环境将加载。 例如，如果使用 MSIL 编写程序，则将调用公共语言运行时来运行程序。

    \- 或 -

    如果未指定 DE，端口将调用操作系统来启动程序，这会导致程序的运行时环境加载。

   > [!NOTE]
   > 如果使用 DE 来启动程序，则可能会将相同的 DE 附加到程序。

3. 根据是否已启动程序，取消运行或运行时环境，然后创建程序说明或节点，并通知端口正在运行的端口。

   > [!NOTE]
   > 建议运行时环境创建程序节点，因为程序节点是可进行调试的程序的轻型表示形式。 无需加载整个 DE 即可创建和注册程序节点。 如果 DE 设计为在 IDE 的进程中运行，但实际上没有运行任何 IDE，则需要有一个可以将程序节点添加到端口的组件。

   在同一个 IDE 中，新创建的程序以及任何其他程序（相关或无关的）已启动或附加到，构成调试会话。

   以编程方式，当用户第一次按 **F5** 时， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试包将调用与通过方法) 所启动程序的类型相关联 (的项目包 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> ，后者又 <xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2> 使用解决方案的活动项目调试设置来填充结构。 此结构通过调用方法传递回调试包 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A> 。 然后，调试包将实例化会话调试管理器 (SDM) ，后者启动正在调试的程序以及任何关联的调试引擎。

   传递给 SDM 的参数之一是要用于启动程序的 DE 的 GUID。

   如果解除 GUID 不是 `GUID_NULL` ，则 SDM 将创建 de，然后调用其 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) 方法以启动程序。 例如，如果程序是用本机代码编写的， `IDebugEngineLaunch2::LaunchSuspended` 则可能会调用 `CreateProcess` 并 `ResumeThread` (Win32 函数) 运行程序。

   作为启动程序的结果，将加载程序的运行时环境。 然后，"DE" 或 "运行时" 环境会创建一个 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 接口用于描述程序，并将此接口传递到 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) ，以通知端口程序正在运行。

   如果 `GUID_NULL` 传递了，则端口启动程序。 程序运行后，运行时环境将创建一个 `IDebugProgramNode2` 接口，用于描述程序并将其传递给 `IDebugPortNotify2::AddProgramNode` 。 这会通知端口该程序正在运行。 然后，SDM 将调试引擎附加到正在运行的程序。

## <a name="in-this-section"></a>在本节中
 [通知端口](../../extensibility/debugger/notifying-the-port.md) 说明启动程序并通知端口后会发生的情况。

 [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md) 当调试会话准备好将 DE 附加到程序时进行记录。

## <a name="related-sections"></a>相关章节
 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务的链接，如启动程序和计算表达式。
