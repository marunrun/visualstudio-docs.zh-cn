---
title: IDE 定义的命令、菜单和组 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6557f49b019a6793698dabe852919ec2e9f28cfd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707721"
---
# <a name="ide-defined-commands-menus-and-groups"></a>IDE 定义的命令、菜单和组
许多菜单、命令和命令组已定义供[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 使用。 这些命令在扩展[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]时也可用于使用。

## <a name="finding-environment-defined-commands"></a>查找环境定义的命令
 环境命令由四个 .vsct 文件组定义：

- 共享 CmdDef.vsct

- 共享 CmdPlace.vsct

- 壳牌CmdDef.vsct

- 壳牌CmdPlace.vsct

  这些文件位于\\*\<视觉工作室 SDK 安装路径>*[VisualStudio 集成]公共\Inc。 这些文件提供菜单和组的定义和 GUID，您可以在 VSPackage 的命令表配置 （.vsct） 文件中用作您自己的菜单、组和命令的容器。

## <a name="in-this-section"></a>本节内容
- [Visual Studio 菜单中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)

 在 Visual Studio 菜单栏上提供菜单及其包含的组的 GUID 和 ID 值。

- [Visual Studio 工具栏中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

 提供可视化工作室 IDE 中工具栏及其包含组的 GUID 和 ID 值。

- [Visual Studio 命令中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)

 提供可视化工作室 IDE 定义的命令的 GUID 和 ID 值。

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [用于扩展项目系统的 IDE 定义的命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
