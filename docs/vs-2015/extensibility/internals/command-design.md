---
title: 命令设计 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands
- commands, implementation
ms.assetid: 097108c3-f758-4b87-89d6-b32d12d9041a
caps.latest.revision: 35
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a6e9eaf69be62b38a880b07fd8eb51cfc9c256a3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195079"
---
# <a name="command-design"></a>命令设计
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当将命令添加到 VSPackage 时，必须指定它的位置显示、 时可用，和它的方式进行处理。  
  
## <a name="defining-commands"></a>定义命令  
 若要定义新的命令，请在 VSPackage 项目中包含的 Visual Studio 命令表格 (.vsct) 文件。 如果你已使用 Visual Studio 包模板创建 VSPackage，该项目包括这些文件之一。 有关详细信息，请参阅 [Visual Studio Command Table (.Vsct) Files](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。  
  
 Visual Studio 将发现，以便它可以显示命令的所有.vsct 文件都合并。 因为这些文件是不同于二进制 VSPackage，则不需要为了查找的命令将包加载 Visual Studio。 有关详细信息，请参阅[如何 Vspackage 添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。  
  
 Visual Studio 将使用<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>注册属性来定义的菜单资源和命令。 有关详细信息，请参阅[实现](../../extensibility/internals/command-implementation.md)。  
  
 在许多不同的方式，可以在运行时更改命令。 它们可以显示或隐藏、 启用或禁用。 它们可以显示不同的文本或图标，或包含不同的值。 可能会先执行大量的自定义 Visual Studio 将加载你的 VSPackage。 有关详细信息，请参阅[如何 Vspackage 添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。  
  
## <a name="command-handlers"></a>命令处理程序  
 在创建命令时，必须提供一个事件处理程序，以执行命令。 如果用户选择该命令，它必须将相应地路由。 路由命令意味着将其发送到正确的 VSPackage 可以启用或禁用它，隐藏或显示，并执行它，如果用户选择要执行此操作。 有关详细信息，请参阅[路由算法](../../extensibility/internals/command-routing-algorithm.md)。  
  
## <a name="the-visual-studio-command-environment"></a>Visual Studio 命令环境  
 Visual Studio 可以承载任意数量的 Vspackage，以及每个可以参与其自身的命令集。 环境显示仅适用于当前任务的命令。 有关详细信息，请参阅[可用性](../../extensibility/internals/command-availability.md)并[选择上下文对象](../../extensibility/internals/selection-context-objects.md)。  
  
 定义新的命令、 菜单、 工具栏或快捷菜单的 VSPackage 提供其命令信息到 Visual Studio 在安装时，通过引用本机或托管程序集中的资源的注册表项。 然后，每个资源引用时编译的 Visual Studio 命令表格 (.vsct) 文件生成的二进制数据资源 (.cto) 文件。 这使 Visual Studio，而无需加载每个已安装的 VSPackage 提供合并的命令集、 菜单和工具栏。  
  
### <a name="command-organization"></a>命令组织  
 在环境定位按组、 优先级别和菜单命令。  
  
- 组是逻辑集合的相关命令，例如，则**剪切**，**副本**，并**粘贴**命令组。 组是显示在菜单的命令。  
  
- 优先级确定在组中的单个命令的菜单的显示的顺序。  
  
- 菜单作为容器的组。  
  
  某些命令、 组和菜单，预定义环境。 有关详细信息，请参阅[默认命令、 组和工具栏位置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)。  
  
  命令可以分配给主组。 主要组控制的命令在主菜单结构和位置**自定义**对话框。 命令可以出现在多个组;例如，命令可以是主菜单、 快捷菜单和工具栏。 有关详细信息，请参阅[如何 Vspackage 添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)。  
  
### <a name="command-routing"></a>命令传送  
 调用和 Vspackage 的路由命令的过程不同于对象实例上调用方法的过程。  
  
 环境将路由到最外面的 （全局） 上下文命令按顺序从最内部的 （本地） 命令上下文，它基于当前所选内容。 无法执行该命令的第一个上下文是对其进行处理。 有关详细信息，请参阅[路由算法](../../extensibility/internals/command-routing-algorithm.md)。  
  
 在大多数情况下，环境处理命令通过使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。 命令路由方案使许多不同的对象以处理命令，因为<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>可以实现任意数量的对象; 这包括 Microsoft ActiveX 控件、 窗口视图实现，文档对象、 项目层次结构和 （适用于全局命令） VSPackage 对象本身。 在某些特殊情况下，例如，将路由在层次结构中，命令<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>必须实现接口。  
  
## <a name="related-topics"></a>相关主题  
  
|Title|描述|  
|-----------|-----------------|  
|[实现](../../extensibility/internals/command-implementation.md)|介绍如何在 VSPackage 中实现命令。|  
|[可用性](../../extensibility/internals/command-availability.md)|介绍 Visual Studio 上下文如何确定有哪些命令。|  
|[路由算法](../../extensibility/internals/command-routing-algorithm.md)|介绍 Visual Studio 命令路由体系结构如何使命令来处理不同的 Vspackage。|  
|[放置指南](../../extensibility/internals/command-placement-guidelines.md)|建议如何在 Visual Studio 环境中放置命令。|  
|[VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)|介绍 Vspackage 如何充分利用 Visual Studio 命令体系结构。|  
|[默认命令、组和工具栏位置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)|介绍 Vspackage 如何充分利用 Visual Studio 中包含的命令。|  
|[管理 VSPackages](../../extensibility/managing-vspackages.md)|介绍 Visual Studio 加载 Vspackage 的方式。|  
|[Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|提供了有关基于 XML 的.vsct 文件，用于描述的布局和外观的 Vspackage 中的命令的信息。|
