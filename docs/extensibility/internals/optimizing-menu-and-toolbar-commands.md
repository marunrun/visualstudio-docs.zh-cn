---
title: 优化菜单和工具栏命令 |微软文档
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
ms.openlocfilehash: 4932a4404c3d76b089468864f84d011524e9cfa0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706909"
---
# <a name="optimizing-menu-and-toolbar-commands"></a>优化菜单和工具栏命令
VSPackages 及其相应的命令的添加[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可能会导致 UI 拥挤。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供了帮助最小化 UI 命令混淆的方法。

## <a name="in-this-section"></a>本节内容
- [提供可用命令](../../extensibility/internals/making-commands-available.md)

 提供添加 VS 包时最小化[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI 挤拥的一般准则。

- [放置指南](../../extensibility/internals/command-placement-guidelines.md)

 提供根据命令集的大小实现 VSPackage 的特定准则。

## <a name="related-sections"></a>相关章节
- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

 说明如何创建包含菜单、工具栏和命令组合框的 UI。
