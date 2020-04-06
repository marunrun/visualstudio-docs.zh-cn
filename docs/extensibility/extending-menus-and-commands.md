---
title: 扩展菜单和命令 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dfcedd3f1b4cb48631541f1726556dab766402ab
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711802"
---
# <a name="extend-menus-and-commands"></a>扩展菜单和命令
命令是向可视化工作室添加操作和进程的方式。 在大多数情况下，命令显示在菜单或工具栏上。 VSPackage 项目模板演示如何实现非常基本的命令。 有关稍长但仍处于基本实现的时间，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

 有关 Visual Studio 命令、菜单和工具栏的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

 命令、菜单和工具栏在作为 VSPackage 项目的一部分的 *.vsct*文件中定义。 您可以在[VS包如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)中找到有关 Visual Studio IDE 和 *.vsct*文件的信息。

 以下主题说明如何添加不同类型的命令、菜单和工具栏。

## <a name="in-this-section"></a>在本节中
- [向视觉工作室菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)说明如何向顶部 Visual Studio 菜单栏添加菜单。

- [将键盘快捷键绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)说明如何向菜单项添加键盘快捷方式（如 CTRL + 3）。

- [向菜单添加子菜单](../extensibility/adding-a-submenu-to-a-menu.md)说明如何向顶部菜单添加子菜单。

- [将最近使用的列表添加到子菜单](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)说明如何添加最近使用的列表。

- [创建可重用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md)描述如何对命令项进行分组，以便它们可以包含在多个菜单上。

- [向菜单命令添加图标](../extensibility/adding-icons-to-menu-commands.md)描述如何向工具栏和菜单上的命令添加图标。

- [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)描述使用`TextChanges`标志以启用动态更改菜单项。

- [更改命令的外观](../extensibility/changing-the-appearance-of-a-command.md)描述如何动态启用或禁用命令。

- [更新用户界面](../extensibility/updating-the-user-interface.md)描述如何强制更新用户界面以反映最近的更改。

- [本地化菜单命令](../extensibility/localizing-menu-commands.md)说明如何本地化菜单命令。
