---
title: 使用互操作程序集的命令和菜单 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ad6b324953914df7103d0dec7371199e3cbbd937
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195046"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>使用互操作程序集的命令和菜单
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

通过使用互操作程序集来实现菜单和工具栏命令的 VSPackage 必须：  
  
- 通知[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]有关所支持的命令以及它们当前是否启用的集成的开发环境 (IDE)。  
  
- 遵守的规则 （协定） 处理的命令。  
  
- 显式实现通过使用命令处理<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口。  
  
  下面介绍如何执行这些任务。  
  
## <a name="in-this-section"></a>本节内容  
 [使用互操作程序集确定命令状态](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)  
 介绍 VSPackage 如何通知 IDE 有关哪些命令它支持以及它们当前是否启用。  
  
 [互操作程序集中的命令协定](../../extensibility/internals/command-contracts-in-interop-assemblies.md)  
 提供了所有的 Vspackage 实现命令使用互操作程序集使用的基本命令协定的定义  
  
 [实现](../../extensibility/internals/command-implementation.md)  
 概述如何 VSPackage 实现命令。  
  
 [注册互操作程序集命令处理程序](../../extensibility/internals/registering-interop-assembly-command-handlers.md)  
 介绍通知 IDE VSPackage 提供的命令处理程序所需的注册表项。  
  
## <a name="related-sections"></a>相关章节  
 [可用性](../../extensibility/internals/command-availability.md)  
 描述 IDE 用于确定哪些 VSPackage 命令可供和哪些对象将处理它们的条件。  
  
 [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)  
 提供了有关如何创建一个用户界面，使用的详细信息[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]命令的支持。  
  
 [VSPackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)  
 用于使具有正确的命令请求的对象的相关过程的概述。
