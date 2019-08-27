---
title: 命令的 Vspackage 中的路由 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing, Visual Studio SDK
ms.assetid: a9c7f9ae-3594-4557-a314-8cf76f5f8772
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a534a015f57a738ca65895002a6fec4454f0ae97
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342229"
---
# <a name="command-routing-in-vspackages"></a>Vspackage 中的命令传送
命令路由中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]基于在其中执行的上下文。 它从初始上下文外部路由到全局上下文。

## <a name="in-this-section"></a>本节内容
- [命令传送算法](../../extensibility/internals/command-routing-algorithm.md)

 描述命令路由解析的顺序。

- [命令可用性](../../extensibility/internals/command-availability.md)

 讨论命令路由。

- [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 讨论托管的代码和 COM 之间的路由命令中的注意事项

## <a name="related-sections"></a>相关章节
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)

 讨论如何确定用户的选定内容上下文焦点窗口上的模型。

- [命令、 菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

 说明如何创建包含菜单、工具栏和命令组合框的 UI。