---
title: 默认命令、组和工具栏放置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b432b514231e876dda1393bad8a315030272d998
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708890"
---
# <a name="default-command-group-and-toolbar-placement"></a>默认命令、组和工具栏放置
为使产品均匀性和稳定性，UI 默认显示某些命令组，并为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]命令和命令组提供定义。 VS包也可以使用标准命令和命令组。

 默认命令组分为三类：IDE 命令、产品命令和编辑器命令。

## <a name="default-ide-commands"></a>默认 IDE 命令
 默认 IDE 工具栏包括 由 中包含的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]所有产品共享的命令。 其中包括与通用项目操作相关的命令，如 **"保存"** 命令和 **"添加项目"** 命令。 VSPackages 不应从此工具栏中添加或减去，但有一个例外：如果产品或 VSPackage 添加了新的工具窗口，则应将窗口添加到 **"视图"** 菜单上的可用工具窗口列表中。 新产品或 VS 包可以添加自己的工具栏。

## <a name="default-product-commands"></a>默认产品命令
 每个产品都可以为 IDE 提供其自己的默认工具栏，其中包含重要且经常使用的命令。 但是，最好尽可能使用现有菜单和工具栏，并根据需要使用其他特定于任务的工具栏对其进行补充。

 工具栏的优先级字段确定其行位置。 零优先级将工具栏放在第三行（第 3 行）、菜单栏（第 1 行）和**标准**工具栏（第 2 行）下方。 因此，其他工具栏出现在行（优先级 = 3）。 如果有空间，则后续工具栏将放在同一行上;否则，它们将自动移动到下一行。

## <a name="default-editor-commands"></a>默认编辑器命令
 提供自定义编辑器的 VSPackage 应提供默认工具栏，其中包含该编辑器中最重要且最常用的命令。 编辑器工具栏应在编辑器处于活动状态时显示，并且在编辑器不处于活动状态时应隐藏。 此可见性控制在`VisibilityConstraints`*.vsct*文件的元素中。

 编辑器工具栏应放在 IDE 和产品工具栏下方。

## <a name="see-also"></a>请参阅
- [IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)
- [VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
