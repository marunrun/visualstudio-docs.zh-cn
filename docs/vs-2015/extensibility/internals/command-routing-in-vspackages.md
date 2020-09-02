---
title: Vspackage 中的命令传送 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing, Visual Studio SDK
ms.assetid: a9c7f9ae-3594-4557-a314-8cf76f5f8772
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 954d3f25a425652d8adcb31bd36fab06de0d04d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195088"
---
# <a name="command-routing-in-vspackages"></a>VSPackage 中的命令传送
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

命令 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 根据执行它的上下文进行路由。 它从初始上下文到全局上下文的外部路由。  
  
## <a name="in-this-section"></a>本节内容  
 [路由算法](../../extensibility/internals/command-routing-algorithm.md)  
 描述命令路由解决方案的顺序。  
  
 [可用性](../../extensibility/internals/command-availability.md)  
 讨论命令路由。  
  
 [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)  
 讨论托管代码与 COM 之间路由命令的注意事项。  
  
## <a name="related-sections"></a>相关章节  
 [选择上下文对象](../../extensibility/internals/selection-context-objects.md)  
 讨论如何在窗口上确定用户的选择上下文焦点的模型。  
  
 [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)  
 说明如何创建包含菜单、工具栏和命令组合框的 UI。
