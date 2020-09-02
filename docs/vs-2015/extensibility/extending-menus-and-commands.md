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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204525"
---
# <a name="extending-menus-and-commands"></a>扩展菜单和命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

命令是向 Visual Studio 添加操作和过程的方式。 在大多数情况下，会在菜单或工具栏上显示命令。 VSPackage 项目模板演示如何实现一个非常基本的命令。 对于稍长但仍是基本实现的，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
 有关 Visual Studio 命令、菜单和工具栏的详细信息，请参阅 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。  
  
 命令、菜单和工具栏是在 VSPackage 项目中的 .vsct 文件中定义的。 可以在 [Vspackage 添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)中找到有关 VISUAL Studio IDE 和 .vsct 文件的信息。  
  
 以下主题介绍如何添加不同种类的命令、菜单和工具栏。  
  
## <a name="in-this-section"></a>本节内容  
 [将菜单添加到 Visual Studio 菜单栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)  
 说明如何向 Visual Studio 的顶部菜单栏添加菜单。  
  
 [将键盘快捷方式绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)  
 说明如何将键盘快捷方式 (如 CTRL + 3) 添加到菜单项。  
  
 [将子菜单添加到菜单](../extensibility/adding-a-submenu-to-a-menu.md)  
 说明如何将子菜单添加到顶部菜单。  
  
 [将最近使用的列表添加到子菜单](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)  
 说明如何添加最近使用的列表。  
  
 [创建可重复使用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md)  
 介绍如何对命令项进行分组，以便可以将它们包含在多个菜单上。  
  
 [将图标添加到菜单命令](../extensibility/adding-icons-to-menu-commands.md)  
 介绍如何将图标添加到工具栏和菜单上的命令。  
  
 [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)  
 描述如何使用 `TextChanges` 标志来使菜单项动态更改。  
  
 [更改命令的外观](../extensibility/changing-the-appearance-of-a-command.md)  
 描述如何动态地启用或禁用命令。  
  
 [更新用户接口](../extensibility/updating-the-user-interface.md)  
 描述如何强制用户界面的更新反映最近的更改。  
  
 [本地化菜单命令](../extensibility/localizing-menu-commands.md)  
 说明如何本地化菜单命令。  
  
## <a name="related-sections"></a>相关章节
