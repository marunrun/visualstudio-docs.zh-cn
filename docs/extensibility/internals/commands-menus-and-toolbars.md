---
title: 命令、 菜单和工具栏 |Microsoft Docs
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
ms.openlocfilehash: aed5a91a819658fb141abb4301b9b9499ed602c6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311163"
---
# <a name="commands-menus-and-toolbars"></a>命令、 菜单和工具栏
菜单和工具栏是用户可访问你的 VSPackage 中的命令。 命令是完成任务（如打印文档、刷新视图或创建新文件）的函数。 菜单和工具栏是用于向用户呈现命令的方便图形方式。 通常，相关命令在相同菜单或工具栏上聚集在一起。

- 菜单通常在集成开发环境 (IDE) 或工具窗口顶部显示为聚集在一行中的一个单词字符串。 菜单还可以显示为右键单击事件的结果，称为该上下文中的快捷菜单。 单击时，菜单会展开以显示一个或多个命令。 命令在单击时可以执行的任务或启动包含其他命令的子菜单。 某些常见的菜单名称不**文件**，**编辑**，**视图**，以及**窗口**。 有关详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

- 工具栏通常是按钮和其他控件（如组合框、列表框、文本框和菜单控制器）组成的行。 所有工具栏控件都与命令关联。 单击工具栏按钮时，会激活其关联命令。 工具栏按钮通常具有提示基础命令的图标，如用于打印命令的打印机。 在下拉列表控件中，列表中的每项都与不同命令关联。 菜单控制器是一种混合体，其中控件的一端是工具栏按钮，另一端是在单击时显示其他命令的向下箭头。 有关详细信息，请参阅[向工具栏添加菜单控制器](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)。

- 创建命令时，还必须为它创建事件处理程序。 事件处理程序确定命令何时可见或启用、使你可以修改其文本并确保命令在激活时以合适方式进行响应（“路由”）。 在大多数情况下，IDE 使用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口处理命令。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中的命令以分层方式进行路由，基于本地选择从最内层命令上下文开始，然后基于全局选择继续执行到最外层上下文。 添加到主菜单的命令可立即用于脚本编写。 有关详细信息，请参阅[MenuCommands 与。OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)并[选择上下文对象](../../extensibility/internals/selection-context-objects.md)。

  若要定义新菜单和工具栏，您必须进行说明 Visual Studio 命令表 ( *.vsct*) 文件。 Visual Studio 包模板创建，以支持任何命令、 工具栏和模板中选择的编辑器所需的元素以及此文件。 或者，您可以编写自己 *.vsct*文件，使用此处所述的 XML 架构：[VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)。

  有关使用详细信息 *.vsct*文件，请参阅[Visual Studio 命令表格 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

  在本部分中的主题介绍在 Vspackage 中的命令、 菜单和工具栏的工作原理。

## <a name="in-this-section"></a>本节内容
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 命令表格式规范进行深入说明。

- [Visual Studio 命令表格 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

 介绍基于 XML 的语法和编译器的命令表。

- [默认命令、 组和工具栏位置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)

 描述了预定义的命令、 组、 菜单和工具栏。

- [IDE 定义的命令、 菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)

 指定预定义的菜单、 命令和命令组可供使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。

- [命令设计](../../extensibility/internals/command-design.md)

 介绍如何设计命令。

- [优化菜单和工具栏命令](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)

 为命令提供了指导。

- [执行的命令](../../extensibility/internals/making-commands-available.md)

 介绍如何向 Visual Studio 提供的命令。

- [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 介绍如何实现使用互操作程序集的命令。

## <a name="related-sections"></a>相关章节
- [Vspackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)

 介绍了在 Vspackage 中路由命令。