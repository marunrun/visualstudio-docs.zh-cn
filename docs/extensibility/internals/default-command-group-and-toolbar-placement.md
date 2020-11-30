---
title: 默认命令、组和工具栏位置 |Microsoft Docs
description: 了解默认情况下 Visual Studio 用户界面显示的 IDE 命令、产品命令和编辑器命令。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: cacf8db933c7d56d44351da11b7b310bc0bdb8aa
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96329875"
---
# <a name="default-command-group-and-toolbar-placement"></a>默认命令、组和工具栏位置
对于产品一致性和稳定性，UI 默认显示特定的命令组，并 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供命令和命令组的定义。 Vspackage 还可以使用标准命令和命令组。

 默认命令组分为三个类别： IDE 命令、产品命令和编辑器命令。

## <a name="default-ide-commands"></a>默认 IDE 命令
 默认 IDE 工具栏包括中包含的所有产品共享的命令 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 其中包括与常规项目操作相关的命令，如 " **保存** " 命令和 " **添加项** " 命令。 Vspackage 不应在此工具栏中增加或减少，但有一个例外：如果产品或 VSPackage 添加新的工具窗口，则应将该窗口添加到 " **视图** " 菜单上的可用工具窗口列表中。 新产品或 Vspackage 可以添加其工具栏。

## <a name="default-product-commands"></a>默认产品命令
 每个产品都可以为 IDE 提供其自己的默认工具栏，其中包含重要的常用命令。 不过，最好尽可能使用现有的菜单和工具栏，并根据需要使用其他特定于任务的工具栏对其进行补充。

 工具栏的 "优先级" 字段决定其行位置。 如果为零，则在第3行 (第3行) ，菜单栏 (行 1) ， **标准** 工具栏 (第2行) 。 因此，其他工具栏出现在 " (优先级 + 3") 行。 如果有空间，后续工具栏会置于同一行;否则，它们会自动移动到下一行。

## <a name="default-editor-commands"></a>默认编辑器命令
 提供自定义编辑器的 VSPackage 应提供一个默认工具栏，其中包含该编辑器中最重要和最常用的命令。 编辑器处于活动状态时应显示编辑器工具栏，当编辑器处于非活动状态时应隐藏编辑器工具栏。 此可见性是在 `VisibilityConstraints` *.vsct* 文件的元素中控制的。

 编辑器工具栏应放置在 IDE 和 product 工具栏下方。

## <a name="see-also"></a>请参阅
- [IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
