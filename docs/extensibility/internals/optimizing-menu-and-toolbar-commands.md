---
title: 优化菜单和工具栏命令 |Microsoft Docs
description: 了解 Visual Studio 如何最大程度地减少因添加 Vspackage 和其相应命令而导致的命令混淆。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], menus
- commands [Visual Studio], toolbars
- menus [Visual Studio SDK], commands
- menu commands, implementing
- toolbars [Visual Studio], commands
ms.assetid: 8385f1a6-1e98-4dca-83d2-fcbed7177242
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b35f3a87f819885685b54888031883f4c2776d04
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877593"
---
# <a name="optimizing-menu-and-toolbar-commands"></a>优化菜单和工具栏命令
添加 Vspackage 及其相应的命令 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可能会导致拥挤的 UI。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供有助于最大程度地减少 UI 命令混淆的方法。

## <a name="in-this-section"></a>本节内容
- [提供可用命令](../../extensibility/internals/making-commands-available.md)

 提供有关在添加 Vspackage 时最大限度地减少 UI crowding 的一般准则 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [放置指南](../../extensibility/internals/command-placement-guidelines.md)

 提供根据命令集的大小实现 VSPackage 的特定准则。

## <a name="related-sections"></a>相关章节
- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

 说明如何创建包含菜单、工具栏和命令组合框的 UI。
