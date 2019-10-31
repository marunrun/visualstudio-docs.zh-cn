---
title: 命令、菜单和工具栏 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- commands [Visual Studio]
- toolbars [Visual Studio], commands
ms.assetid: 07b4ed90-dbbd-40df-b6c9-8395fd6f2ab6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a53b0a4e83b9d8a20efcec20f1362ba5c6647b0
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186694"
---
# <a name="commands-menus-and-toolbars"></a>命令、菜单和工具栏
菜单和工具栏是用户访问 VSPackage 中的命令的方式。 命令是完成任务（如打印文档、刷新视图或创建新文件）的函数。 菜单和工具栏是用于向用户呈现命令的方便图形方式。 通常，相关命令在相同菜单或工具栏上聚集在一起。

- 菜单通常在集成开发环境 (IDE) 或工具窗口顶部显示为聚集在一行中的一个单词字符串。 菜单还可以显示为右键单击事件的结果，称为该上下文中的快捷菜单。 单击时，菜单会展开以显示一个或多个命令。 命令在单击时可以执行的任务或启动包含其他命令的子菜单。 一些常见的菜单名包括**文件**、**编辑**、**视图**和**窗口**。 有关详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

- 工具栏通常是按钮和其他控件（如组合框、列表框、文本框和菜单控制器）组成的行。 所有工具栏控件都与命令关联。 单击工具栏按钮时，会激活其关联命令。 工具栏按钮通常具有提示基础命令的图标，如用于打印命令的打印机。 在下拉列表控件中，列表中的每项都与不同命令关联。 菜单控制器是一种混合体，其中控件的一端是工具栏按钮，另一端是在单击时显示其他命令的向下箭头。 有关详细信息，请参阅[向工具栏添加菜单控制器](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)。

- 创建命令时，还必须为它创建事件处理程序。 事件处理程序确定命令何时可见或启用、使你可以修改其文本并确保命令在激活时以合适方式进行响应（“路由”）。 在大多数情况下，IDE 使用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口处理命令。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中的命令以分层方式进行路由，基于本地选择从最内层命令上下文开始，然后基于全局选择继续执行到最外层上下文。 添加到主菜单的命令可立即用于脚本编写。 有关详细信息，请参阅[menucommand 和 OleMenuCommands](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)以及[选择上下文对象](../../extensibility/internals/selection-context-objects.md)。

  若要定义新的菜单和工具栏，必须在 Visual Studio 命令表（ *.vsct*）文件中进行描述。 Visual Studio 包模板会为你创建此文件，以及支持你在模板中选择的任何命令、工具栏和编辑器所需的元素。 或者，您可以使用此处所述的 XML 架构编写您自己的 *.vsct*文件： [.vsct XML schema reference](../../extensibility/vsct-xml-schema-reference.md)。

  有关使用 *.vsct*文件的详细信息，请参阅[Visual Studio 命令表（.vsct）文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

  本节中的主题介绍如何在 Vspackage 中使用命令、菜单和工具栏。

## <a name="in-this-section"></a>本节内容
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 命令表格格式规范的详细说明。

- [Visual Studio 命令表（.vsct）文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

 描述用于命令表的基于 XML 的语法和编译器。

- [默认命令、组和工具栏位置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)

 介绍预定义的命令、组、菜单和工具栏。

- [IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)

 指定可供 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 使用的预定义菜单、命令和命令组。

- [命令设计](../../extensibility/internals/command-design.md)

 说明如何设计命令。

- [优化菜单和工具栏命令](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)

 提供命令的指导原则。

- [使命令可用](../../extensibility/internals/making-commands-available.md)

 说明如何使命令可用于 Visual Studio。

- [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 说明如何实现使用互操作程序集的命令。

## <a name="related-sections"></a>相关章节
- [Vspackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)

 说明 Vspackage 中的命令路由。