---
title: 命令放置指南 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709567"
---
# <a name="command-placement-guidelines"></a>命令放置指南
在 Visual Studio 集成开发环境 （IDE） 中定位命令的最佳做法因命令集的大小而异。 命令根据 *.vsct*文件中的信息定义和定位。

## <a name="best-practices-for-all-command-sets"></a>所有命令集的最佳做法
 对于每组命令，请遵循以下准则：

- 提前准备命令结构图表。 标识将在多个位置使用的命令、组合框、命令组和快捷菜单。

- 出现在同一组中的命令应相关。

- 只包含一个命令的组是可以接受的。

- 包不应向现有 Visual Studio 菜单添加大量命令。 相反，他们应该创建菜单或子菜单来承载新命令。

- 将命令放在现有菜单上时，命名该命令，使其用途明确，并且不会与现有命令混淆。

## <a name="best-practices-for-small-command-sets"></a>小型命令集的最佳做法
 如果您正在开发一个仅包含几个命令的 VSPackage，请遵循以下准则：

- 如果可能，请使用命令、组合框、组或子菜单的[父](../../extensibility/parent-element.md)元素将其放入相应的组中。

- 将这些组分配给 VSPackage 显示的菜单。

- 子菜单或命令的父级必须是[组](../../extensibility/group-element.md)元素。 将命令和子菜单分配给组，然后将组分配给父菜单。

- 通过在命令定义后添加[命令放置](../../extensibility/commandplacements-element.md)元素部分，然后将命令添加到`CommandPlacements`元素中，从而将命令放入其他组中。 [CommandPlacement](../../extensibility/commandplacement-element.md)

## <a name="best-practices-for-large-command-sets"></a>大型命令集的最佳做法
 如果您的 VSPackage 将有许多命令将显示在多个上下文中，请遵循以下准则：

- 使菜单、组和命令自父母。 也就是说，不要在项的定义中`Parent`分配元素。

- 使用`CommandPlacement``CommandPlacements`元素部分中的元素条目将菜单、组和命令放在其父菜单和组中。

- 在`CommandPlacements`元素部分中，填充给定菜单或组的条目应彼此相邻。 这有助于可读性，`Priority`使排名更容易确定。

## <a name="see-also"></a>请参阅
- [VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
