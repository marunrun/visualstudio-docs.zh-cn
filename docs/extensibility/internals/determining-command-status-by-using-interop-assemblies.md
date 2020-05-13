---
title: 使用互操作程序集确定命令状态 |微软文档
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
ms.openlocfilehash: 52bea32997b083cd13349a37201411e357f94a90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708703"
---
# <a name="determine-command-status-by-using-interop-assemblies"></a>使用互操作程序集确定命令状态
VSPackage 必须跟踪它可以处理的命令的状态。 环境无法确定在 VSPackage 中处理的命令何时启用或禁用。 VSPackage 负责通知环境命令状态，例如，常规命令的状态，如**剪切**、**复制**和**粘贴**。

## <a name="status-notification-sources"></a>状态通知源
 环境通过 VSPackage<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法接收有关命令的信息，这是 VSPackage 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口的一部分。 环境在<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>以下两种情况下调用 VSPackage 的方法：

- 当用户打开主菜单或上下文菜单（通过右键单击）时，环境将执行该菜单上所有命令<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>上的方法以确定其状态。

- 当 VS 包请求环境更新当前用户界面 （UI） 时。 此更新作为当前对用户可见的命令（如标准工具栏上的**剪切**、**复制**和**粘贴**分组）而启用和禁用，以响应上下文和用户操作。

  由于 shell 承载多个 VSPackage，因此，如果需要轮询每个 VSPackage 以确定命令状态，则 shell 的性能将不可接受。 相反，当更改时，VSPackage 应主动通知环境。当其 UI 发生更改时。 有关更新通知的详细信息，请参阅[更新用户界面](../../extensibility/updating-the-user-interface.md)。

## <a name="status-notification-failure"></a>状态通知失败
 VSPackage 未能通知环境命令状态更改可能会使 UI 处于不一致状态。 请记住，用户可以将任何菜单或上下文菜单命令放在工具栏上。 因此，仅在打开菜单或上下文菜单时更新 UI 是不够的。

## <a name="see-also"></a>请参阅
- [VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [实现](../../extensibility/internals/command-implementation.md)
