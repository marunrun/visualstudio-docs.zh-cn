---
title: 命令放置指南 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5d88a477403c98ff11c5f7303b55f5eb713b668c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195101"
---
# <a name="command-placement-guidelines"></a>命令放置指南
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

最佳做法，用于在 Visual Studio 集成的开发环境 (IDE) 中定位命令根据命令集的大小会有所不同。 命令定义，并根据.vsct 文件中的信息调整位置。  
  
## <a name="best-practices-for-all-command-sets"></a>所有命令集的最佳实践  
 每个组的命令，请遵循以下准则：  
  
- 提前准备命令结构的图表。 标识命令、 组合框、 命令组和将多个位置中使用的快捷菜单。  
  
- 应与在同一组中显示的命令。  
  
- 包含一个命令的组是可接受的。  
  
- 包不应将很多命令添加到现有的 Visual Studio 菜单。 相反，它们应创建菜单或子菜单来托管新的命令。  
  
- 当将一个命令在现有的菜单上，命令名称，以便清除其用途且不会与现有命令混淆。  
  
## <a name="best-practices-for-small-command-sets"></a>对于较小的命令集的最佳实践  
 如果你要开发具有几个命令的 VSPackage，还请遵循以下准则：  
  
- 如果可能，请使用[父元素](../../extensibility/parent-element.md)命令、 组合框、 组或子菜单将其放在相应的组。  
  
- 将这些组分配到 VSPackage 所显示的菜单。  
  
- 必须为子菜单或命令的父[组元素](../../extensibility/group-element.md)。 将命令和子菜单分配给组，然后将组分配给父菜单。  
  
- 您可以将命令放在其他组中通过添加[CommandPlacements 元素](../../extensibility/commandplacements-element.md)后的命令，定义部分，然后将添加到`CommandPlacements Element` [CommandPlacement 元素](../../extensibility/commandplacement-element.md)为每个其他组。  
  
## <a name="best-practices-for-large-command-sets"></a>对于较大的命令集的最佳实践  
 如果你的 VSPackage 将具有多个命令将显示在多个上下文中，还请遵循以下准则：  
  
- 请菜单、 组和命令自作为父级。 也就是说，不要分配`Parent Element`中的项定义。  
  
- 使用`CommandPlacement Element`中的条目`CommandPlacements Element`部分，以将菜单、 组和命令放在其父菜单和组。  
  
- 在`CommandPlacements`部分填充给定的菜单项或组应该彼此相邻。 这有助于提高可读性，并使`Priority`排名更容易地确定。  
  
## <a name="see-also"></a>请参阅  
 [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
