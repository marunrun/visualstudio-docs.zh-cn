---
title: 使用互操作程序集确定命令状态 |Microsoft Docs
description: 了解如何通过使用 IOleCommandTarget 接口来确定在 VSPackage 中处理的命令的 "状态"。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e46252cea550a2caaa81c92853220db4fa2b5b1a
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328374"
---
# <a name="determine-command-status-by-using-interop-assemblies"></a>使用互操作程序集确定命令状态
VSPackage 必须跟踪它可以处理的命令的状态。 环境无法确定在 VSPackage 中处理的命令何时启用或禁用。 VSPackage 负责通知环境有关命令状态的信息，例如， **剪切**、 **复制** 和 **粘贴** 等常规命令的状态。

## <a name="status-notification-sources"></a>状态通知源
 环境通过 Vspackage 的方法接收有关命令的信息 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> ，该方法是接口的 VSPackage 实现的一部分 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>在以下两种情况下，环境将调用 VSPackage 的方法：

- 当用户通过右键单击) 打开主菜单或上下文菜单 (，环境将对 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 该菜单上的所有命令执行方法以确定其状态。

- 当 VSPackage 请求环境更新当前用户界面时)  (UI。 此更新以当前对用户可见的命令进行，如 "标准" 工具栏上的 " **剪切**"、" **复制**" 和 " **粘贴** " 分组，为响应上下文和用户操作而启用和禁用。

  由于 shell 托管多个 Vspackage，因此如果需要轮询每个 VSPackage 来确定命令状态，shell 的性能将会降低。 相反，当发生更改时，VSPackage 应主动通知环境的 UI 更改。 有关更新通知的详细信息，请参阅 [更新用户界面](../../extensibility/updating-the-user-interface.md)。

## <a name="status-notification-failure"></a>状态通知失败
 如果 VSPackage 无法通知环境的命令状态更改，则可能会将 UI 置于不一致的状态。 请记住，用户可以将任何菜单或上下文菜单命令放置在工具栏上。 因此，仅当菜单或上下文菜单打开时，才更新 UI。

## <a name="see-also"></a>请参阅
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [实现](../../extensibility/internals/command-implementation.md)
