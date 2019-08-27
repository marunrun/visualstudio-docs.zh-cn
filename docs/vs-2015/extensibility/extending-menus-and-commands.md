---
title: 扩展菜单和命令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
caps.latest.revision: 50
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 83d9dc45863f1ed1b5e11c17b9e922b62b0186dc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204525"
---
# <a name="extending-menus-and-commands"></a>扩展菜单和命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

命令是将操作和进程添加到 Visual Studio 的方式。 在大多数情况下菜单或工具栏上显示命令。 VSPackage 项目模板演示如何实现一个非常基本命令。 有关稍长，但仍基本实现，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
 有关 Visual Studio 命令、 菜单和工具栏的详细信息，请参阅[命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。  
  
 VSPackage 项目的一部分的.vsct 文件中定义的命令、 菜单和工具栏。 您可以找到有关 Visual Studio IDE 和.vsct 文件中的信息[如何 Vspackage 添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)。  
  
 以下主题介绍如何添加不同类型的命令、 菜单和工具栏。  
  
## <a name="in-this-section"></a>本节内容  
 [将菜单添加到 Visual Studio 菜单栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)  
 介绍如何将菜单添加到 Visual Studio 菜单栏的顶部。  
  
 [将键盘快捷方式绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)  
 介绍如何将键盘快捷方式 （如 CTRL + 3） 添加到菜单项。  
  
 [将子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)  
 介绍如何将子菜单添加到顶部的菜单。  
  
 [将最近使用的列表添加到子菜单](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)  
 介绍如何添加最近使用列表。  
  
 [创建可重复使用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md)  
 介绍如何进行分组，以便可以将它们包含在多个菜单命令项。  
  
 [将图标添加到菜单命令](../extensibility/adding-icons-to-menu-commands.md)  
 介绍如何将图标添加到上一个工具栏和菜单命令。  
  
 [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)  
 介绍如何使用`TextChanges`标志以启用要动态更改菜单项。  
  
 [更改命令的外观](../extensibility/changing-the-appearance-of-a-command.md)  
 介绍如何动态启用或禁用命令。  
  
 [更新用户界面](../extensibility/updating-the-user-interface.md)  
 介绍如何强制进行更新以反映最新更改的用户界面。  
  
 [本地化菜单命令](../extensibility/localizing-menu-commands.md)  
 介绍如何本地化菜单命令。  
  
## <a name="related-sections"></a>相关章节
