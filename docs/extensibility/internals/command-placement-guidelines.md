---
title: 命令放置准则 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 021a5fd9f9931e3041a431d211c8ab49978bbbab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709567"
---
# <a name="command-placement-guidelines"></a>命令放置准则
在 Visual Studio 集成开发环境中定位命令的最佳做法 (IDE) 不同，具体取决于命令集的大小。 命令根据 *.vsct* 文件中的信息进行定义和定位。

## <a name="best-practices-for-all-command-sets"></a>所有命令集的最佳实践
 对于每组命令，请遵循以下准则：

- 提前准备命令结构的图表。 标识将在多个位置使用的命令、组合框、命令组和快捷菜单。

- 同一组中出现的命令应该是相关的。

- 只包含一个命令的组是可接受的。

- 包不应向现有 Visual Studio 菜单添加大量命令。 相反，他们应创建菜单或子菜单来托管新命令。

- 将命令置于现有菜单上时，请将命令命名为，使其目的清晰，并且不会与现有命令混淆。

## <a name="best-practices-for-small-command-sets"></a>小型命令集的最佳实践
 如果要开发只包含几个命令的 VSPackage，也请遵循以下准则：

- 如果可能，请使用命令、组合框、组或子菜单的 [父](../../extensibility/parent-element.md) 元素将其放入相应的组中。

- 将这些组分配给 VSPackage 显示的菜单。

- 子菜单或命令的父项必须是 [组](../../extensibility/group-element.md) 元素。 向组分配命令和子菜单，然后将组分配到父菜单。

- 可以通过在该命令的定义后添加 [CommandPlacements](../../extensibility/commandplacements-element.md) 元素部分，然后向 `CommandPlacements` 元素添加每个其他组的 [CommandPlacement](../../extensibility/commandplacement-element.md) 元素，从而将命令放在其他组中。

## <a name="best-practices-for-large-command-sets"></a>大型命令集的最佳实践
 如果你的 VSPackage 将有许多命令，这些命令将出现在多个上下文中，也请遵循以下准则：

- 使菜单、组和命令自父级。 也就是说，不要 `Parent` 在项的定义中分配元素。

- 使用 `CommandPlacement` 元素部分中的元素项 `CommandPlacements` 可在其父菜单和组中放置菜单、组和命令。

- 在 `CommandPlacements` 元素部分，填充给定菜单或组的项应相邻。 这有助于提高可读性，并使 `Priority` 排名更易于确定。

## <a name="see-also"></a>另请参阅
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Visual Studio 命令表 ( .vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
