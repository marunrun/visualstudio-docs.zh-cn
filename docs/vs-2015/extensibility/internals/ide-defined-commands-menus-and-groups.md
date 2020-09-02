---
title: IDE 定义的命令、菜单和组 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 32e8135328c11fd74311371d07645a525426371e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192739"
---
# <a name="ide-defined-commands-menus-and-groups"></a>IDE 定义的命令、菜单和组
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

许多菜单、命令和命令组已定义为供 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE 使用。 扩展时，还可以使用这些命令 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
## <a name="finding-environment-defined-commands"></a>查找环境定义的命令  
 环境命令在一组 .vsct 文件中定义：  
  
- SharedCmdDef. .vsct  
  
- SharedCmdPlace. .vsct  
  
- ShellCmdDef. .vsct  
  
- ShellCmdPlace. .vsct  
  
  这些文件位于 \VisualStudioIntegration\Common\Inc 中 *\<Visual Studio SDK installation path>* \\ 。 这些文件提供菜单和组的定义和 Guid，可在命令表配置 (. .vsct) 文件中使用，作为你自己的菜单、组和命令的容器。  
  
## <a name="in-this-section"></a>本节内容  
 [Visual Studio 菜单中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)  
 提供 Visual Studio 菜单栏上的菜单的 GUID 和 ID 值以及它们所包含的组的值。  
  
 [Visual Studio 工具栏中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)  
 在 Visual Studio IDE 中提供工具栏的 GUID 和 ID 值，并为其所包含的组提供这些值。  
  
 [Visual Studio 命令中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)  
 提供 Visual Studio IDE 定义的命令的 GUID 和 ID 值。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表 (。.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [IDE 定义的用于扩展项目系统的命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)   
 [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
