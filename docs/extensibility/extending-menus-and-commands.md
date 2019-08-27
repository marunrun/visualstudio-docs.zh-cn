---
title: 扩展菜单和命令 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d0810e1fde5b58416b94607dccf2004fe7edb67b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341145"
---
# <a name="extend-menus-and-commands"></a>扩展菜单和命令
命令是将操作和进程添加到 Visual Studio 的方式。 在大多数情况下菜单或工具栏上显示命令。 VSPackage 项目模板演示如何实现一个非常基本命令。 有关稍长，但仍基本实现，请参阅[与菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

 有关 Visual Studio 命令、 菜单和工具栏的详细信息，请参阅[命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

 中定义的命令、 菜单和工具栏 *.vsct*文件，它是作为 VSPackage 项目的一部分。 你可以找到有关 Visual Studio IDE 信息并 *.vsct*中的文件[Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)。

 以下主题介绍如何添加不同类型的命令、 菜单和工具栏。

## <a name="in-this-section"></a>本节内容
- [向 Visual Studio 菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)介绍了如何将菜单添加到顶级的 Visual Studio 菜单栏。

- [将键盘快捷方式绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)到菜单项说明如何添加键盘快捷方式 （如 CTRL + 3）。

- [将子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)介绍了如何将子菜单添加到顶部的菜单。

- [将最近使用的列表添加到子菜单](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)介绍如何添加最近使用列表。

- [创建可重用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md)介绍了如何进行分组，以便可以将它们包含在多个菜单命令项。

- [将图标添加到菜单命令](../extensibility/adding-icons-to-menu-commands.md)介绍了如何将图标添加到上一个工具栏和菜单命令。

- [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)介绍如何使用`TextChanges`标志以启用要动态更改菜单项。

- [更改命令的外观](../extensibility/changing-the-appearance-of-a-command.md)介绍如何动态启用或禁用命令。

- [更新用户界面](../extensibility/updating-the-user-interface.md)介绍如何强制进行更新以反映最新更改的用户界面。

- [本地化菜单命令](../extensibility/localizing-menu-commands.md)介绍了如何将本地化菜单命令。