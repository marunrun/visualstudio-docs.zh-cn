---
title: VS 包中的命令路由 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing, Visual Studio SDK
ms.assetid: a9c7f9ae-3594-4557-a314-8cf76f5f8772
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 957ddcca46365a882609c15c96d666c2848ace6c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709558"
---
# <a name="command-routing-in-vspackages"></a>VS 包中的命令路由
命令根据执行命令的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]上下文路由。 它将从初始上下文路由到全局上下文。

## <a name="in-this-section"></a>在本节中
- [命令路由算法](../../extensibility/internals/command-routing-algorithm.md)

 描述命令路由解析的顺序。

- [命令可用性](../../extensibility/internals/command-availability.md)

 讨论命令路由。

- [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 讨论托管代码和 COM 之间路由命令中的注意事项。

## <a name="related-sections"></a>相关章节
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)

 讨论如何确定用户选择上下文对窗口的关注模型。

- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

 说明如何创建包含菜单、工具栏和命令组合框的 UI。
