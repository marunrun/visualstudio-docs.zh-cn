---
title: 命令路由算法 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing
ms.assetid: 998b616b-bd08-45cb-845f-808efb8c33bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af8d3e53e09214ce36a80ca18856085dfb2bb746
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709541"
---
# <a name="command-routing-algorithm"></a>命令路由算法
在 Visual Studio 中，命令由许多不同的组件处理。 命令从最里面的上下文（基于当前选择）路由到最外层（也称为全局）上下文。 有关详细信息，请参阅[命令可用性](../../extensibility/internals/command-availability.md)。

## <a name="order-of-command-resolution"></a>命令解析顺序
 命令通过以下级别的命令上下文传递：

1. 加载项：环境首先向存在的任何加载项提供命令。

2. 优先级命令：这些命令使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget>注册。 它们被调用在 Visual Studio 中的每个命令，并且按注册顺序调用。

3. 上下文菜单命令：首先向提供给上下文菜单的命令目标提供位于上下文菜单上的命令，然后提供给典型的路由。

4. 工具栏设置命令目标：调用 时将注册这些命令目标<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A>。 参数`pCmdTarget`可以是`null`。 如果不是`null`，则此命令目标用于更新所设置工具栏上的任何命令。 如果 shell 正在设置工具栏，则它会将窗口框架作为 传递`pCmdTarget`，以便工具栏上的命令的所有更新都流过窗口框架，即使它不在焦点中也是如此。

5. 工具窗口：工具窗口通常实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>接口，它也应该实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口，以便 Visual Studio 可以在工具窗口处于活动状态窗口时获取命令目标。 但是，如果具有焦点的工具窗口是**Project**窗口，则该命令将路由到所选项<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>的常见父级接口。 如果此选择跨越多个项目，则命令将路由到<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution>层次结构。 接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>包含与<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口上的相应<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>命令类似的 和 方法。

6. 文档窗口：如果命令在其 *.vsct*文件中设置了`RouteToDocs`标志，Visual Studio 会查找文档视图对象上的命令目标，该对象是<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>接口的实例或文档对象的实例（通常是<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>接口或<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>接口）。 如果文档视图对象不支持该命令，Visual Studio 会将命令路由到返回<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>的接口。 （这是文档数据对象的可选接口。

7. 当前层次结构：当前层次结构可以是拥有活动文档窗口的项目或**解决方案资源管理器**中选择的层次结构。 Visual Studio 查找<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>在当前层次结构或活动层次结构上实现的接口。 层次结构应支持每当层次结构处于活动状态时有效的命令，即使项目项的文档窗口具有焦点也是如此。 但是，必须使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口及其<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>及其及其方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>支持仅在**解决方案资源管理器**具有焦点时应用的命令。

     **剪切**、**复制**、**粘贴**、**删除**、**重命名**、**输入**和**双击**命令需要特殊处理。 有关如何在层次结构中处理**删除**和**删除**命令的信息，<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>请参阅接口。

8. 全局：如果命令未由前面提到的上下文处理，Visual Studio 会尝试将其路由到拥有实现接口的命令的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>VSPackage。 如果 VSPackage 尚未加载，则 Visual Studio 调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>该方法时不会加载它。 仅当调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法时，才会加载 VSPackage。

## <a name="see-also"></a>请参阅
- [命令设计](../../extensibility/internals/command-design.md)
