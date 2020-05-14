---
title: 使用互通程序集的命令和菜单 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e6c381abe9b4c6ea2a58342e185d7427fa56a180
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709490"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>使用互通程序集的命令和菜单
使用 Interop 程序集实现菜单和工具栏命令的 VSPackage 必须：

- 告知[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 它支持的命令以及当前是否启用这些命令。

- 遵守处理命令的规则（协定）。

- 使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口显式实现命令处理。

  以下部分介绍如何执行这些任务。

## <a name="in-this-section"></a>在本节中
- [使用互操作程序集确定命令状态](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)

 描述 VSPackage 如何通知 IDE 它支持哪些命令以及当前是否启用这些命令。

- [互通程序集中的命令协定](../../extensibility/internals/command-contracts-in-interop-assemblies.md)

 提供使用 Interop 程序集实现命令的所有 VS 包使用的基本命令协定的定义。

- [命令实现](../../extensibility/internals/command-implementation.md)

 概述 VSPackage 如何实现命令。

- [注册内部操作程序集命令处理程序](../../extensibility/internals/registering-interop-assembly-command-handlers.md)

 描述通知 IDE VSPackage 提供命令处理程序所需的注册表项。

## <a name="related-sections"></a>相关章节
- [命令可用性](../../extensibility/internals/command-availability.md)

 描述 IDE 用于确定哪些 VSPackage 命令可用以及哪个对象处理它们的条件。

- [VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 提供有关如何创建使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]命令支持的 UI 的详细信息。

- [VS 包中的命令路由](../../extensibility/internals/command-routing-in-vspackages.md)

 用于将对象与正确的命令请求相关联的过程的概述。
