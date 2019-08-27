---
title: 命令放置指南 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f4cc3dfa8aaeba01709ae74ca9a1d9d54f3c1743
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342118"
---
# <a name="command-placement-guidelines"></a>命令放置指南
最佳做法，用于在 Visual Studio 集成的开发环境 (IDE) 中定位命令根据命令集的大小会有所不同。 命令定义并根据中的信息定位 *.vsct*文件。

## <a name="best-practices-for-all-command-sets"></a>所有命令集的最佳实践
 每个组的命令，请遵循以下准则：

- 提前准备命令结构的图表。 标识命令、 组合框、 命令组和将多个位置中使用的快捷菜单。

- 应与在同一组中显示的命令。

- 包含一个命令的组是可接受的。

- 包不应将很多命令添加到现有的 Visual Studio 菜单。 相反，它们应创建菜单或子菜单来托管新的命令。

- 当将一个命令在现有的菜单上，命令名称，以便清除其用途且不会与现有命令混淆。

## <a name="best-practices-for-small-command-sets"></a>对于较小的命令集的最佳实践
 如果你要开发具有几个命令的 VSPackage，还请遵循以下准则：

- 如果可能，请使用[父](../../extensibility/parent-element.md)命令、 组合框、 组或子菜单将其放在相应的组的元素。

- 将这些组分配到 VSPackage 所显示的菜单。

- 必须为子菜单或命令的父[组](../../extensibility/group-element.md)元素。 将命令和子菜单分配给组，然后将组分配给父菜单。

- 您可以将命令放在其他组中通过添加[CommandPlacements](../../extensibility/commandplacements-element.md)元素部分中的定义之后的命令，然后将添加到`CommandPlacements`元素[CommandPlacement](../../extensibility/commandplacement-element.md)元素对于每个其他组。

## <a name="best-practices-for-large-command-sets"></a>对于较大的命令集的最佳实践
 如果你的 VSPackage 将具有多个命令将显示在多个上下文中，还请遵循以下准则：

- 请菜单、 组和命令自作为父级。 也就是说，不要分配`Parent`中的项定义元素。

- 使用`CommandPlacement`元素中的条目`CommandPlacements`元素部分将在其父菜单和组中的菜单、 组和命令。

- 在`CommandPlacements`元素部分中，填充给定的菜单或组的条目应彼此相邻。 这有助于提高可读性，并使`Priority`排名更容易地确定。

## <a name="see-also"></a>请参阅
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Visual Studio 命令表格 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)