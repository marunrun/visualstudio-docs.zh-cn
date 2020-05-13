---
title: 命令设计 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- commands, implementation
ms.assetid: 097108c3-f758-4b87-89d6-b32d12d9041a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6aa58813623dc8150cafb4fbfee6496d09f889ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709659"
---
# <a name="command-design"></a>命令设计
将命令添加到 VSPackage 时，必须指定该命令的显示位置、何时可用以及如何处理。

## <a name="define-commands"></a>定义命令
 要定义新命令，请在 VSPackage 项目中包括 Visual Studio 命令表 *（.vsct*） 文件。 如果使用 Visual Studio 程序包模板创建了 VSPackage，则项目包括其中一个文件。 有关详细信息，请参阅[可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

 Visual Studio 合并它找到的所有 *.vsct*文件，以便它可以显示命令。 由于这些文件与 VSPackage 二进制文件不同，因此 Visual Studio 不必加载包来查找命令。 有关详细信息，请参阅[VS 包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。

 Visual Studio<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>使用注册属性定义菜单资源和命令。 有关详细信息，请参阅[命令实现](../../extensibility/internals/command-implementation.md)。

 命令可以在运行时以许多不同的方式更改。 它们可以显示或隐藏、启用或禁用。 它们可以显示不同的文本或图标，或包含不同的值。 在 Visual Studio 加载您的 VSPackage 之前，可能会执行大量自定义。 有关详细信息，请参阅[VS 包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。

## <a name="command-handlers"></a>命令处理程序
 创建命令时，必须提供事件处理程序来执行该命令。 如果用户选择该命令，则必须对其进行适当路由。 路由命令意味着将其发送到正确的 VSPackage 以启用或禁用它、隐藏或显示它，并在用户选择这样做时执行它。 有关详细信息，请参阅[命令路由算法](../../extensibility/internals/command-routing-algorithm.md)。

## <a name="visual-studio-command-environment"></a>可视化工作室命令环境
 Visual Studio 可以承载任意数量的 VS 包，并且每个组件都可以贡献自己的命令集。 环境仅显示适合当前任务的命令。 有关详细信息，请参阅[命令可用性](../../extensibility/internals/command-availability.md)和[选择上下文对象](../../extensibility/internals/selection-context-objects.md)。

 定义新命令、菜单、工具栏或快捷菜单的 VSPackage 通过引用本机或托管程序集中的资源的注册表项，在安装时向 Visual Studio 提供其命令信息。 然后，每个资源引用二进制数据资源 （*.cto*） 文件，该文件是在编译 Visual Studio 命令表 *（.vsct*） 文件时生成的。 这使 Visual Studio 能够提供合并的命令集、菜单和工具栏，而无需加载每个已安装的 VSPackage。

### <a name="command-organization"></a>指挥组织
 环境按组、优先级和菜单定位命令。

- 组是相关命令的逻辑集合，例如"**剪切**"、"**复制**"和 **"粘贴"** 命令组。 组是显示在菜单上的命令。

- 优先级确定组中单个命令在菜单上的显示顺序。

- 菜单充当组的容器。

  环境预定义一些命令、组和菜单。 有关详细信息，请参阅[默认命令、组和工具栏放置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)。

  命令可以分配给主组。 主组控制命令在主菜单结构和 **"自定义"** 对话框中的位置。 命令可以出现在多个组中;但是，命令可以出现在多个组中。例如，命令可以位于主菜单、快捷菜单和工具栏上。 有关详细信息，请参阅[VS 包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。

### <a name="command-routing"></a>命令路由
 VSPackages 的调用和路由命令的过程不同于在对象实例上调用方法的过程。

 环境按顺序将命令从基于当前选择的最内层（局部）命令上下文路由到最外层（全局）上下文。 能够执行命令的第一个上下文是处理该命令的上下文。 有关详细信息，请参阅[命令路由算法](../../extensibility/internals/command-routing-algorithm.md)。

 在大多数情况下，环境使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口处理命令。 由于命令路由方案允许许多不同的对象处理命令，<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>因此可以由任意数量的对象实现;其中包括 Microsoft ActiveX 控件、窗口视图实现、文档对象、项目层次结构和 VSPackage 对象本身（用于全局命令）。 在某些特殊情况下，例如，层次结构中的路由命令，必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[命令实现](../../extensibility/internals/command-implementation.md)|描述如何在 VSPackage 中实现命令。|
|[命令可用性](../../extensibility/internals/command-availability.md)|描述可视化工作室上下文如何确定哪些命令可用。|
|[命令路由算法](../../extensibility/internals/command-routing-algorithm.md)|描述 Visual Studio 命令路由体系结构如何使命令能够由不同的 VS 包处理。|
|[命令放置指南](../../extensibility/internals/command-placement-guidelines.md)|建议如何在可视化工作室环境中放置命令。|
|[VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)|描述 VSPackages 如何最好地利用可视化工作室命令体系结构。|
|[默认命令、组和工具栏放置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)|描述 VS 包如何最好地使用 Visual Studio 中包含的命令。|
|[管理 VSPackage](../../extensibility/managing-vspackages.md)|描述可视化工作室如何加载 VS 包。|
|[可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|提供有关基于 XML*的 .vsct*文件的信息，这些文件用于描述 VS 包中命令的布局和外观。|
