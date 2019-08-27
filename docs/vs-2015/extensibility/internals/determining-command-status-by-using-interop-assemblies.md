---
title: 通过使用互操作程序集确定命令状态 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc67123e082258932ab5df6613941f869d6049a6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196791"
---
# <a name="determining-command-status-by-using-interop-assemblies"></a>使用互操作程序集确定命令状态
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage 必须跟踪的它可以处理的命令的状态。 当启用或禁用你的 VSPackage 中处理的命令变得无法确定在环境。 它是你的 VSPackage 以通知有关命令状态的环境的责任，例如，常规状态命令，如**剪切**，**副本**，并**粘贴**。  
  
## <a name="status-notification-sources"></a>状态通知源  
 在环境接收通过 Vspackage 的命令的相关信息<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法，它是 VSPackage 的实现的一部分的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。 环境调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>下两个条件的 vspackage 的方法：  
  
- 当用户打开主菜单或上下文菜单 （通过右键单击） 时，环境执行<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>上该菜单上的命令，以确定其状态的所有方法。  
  
- 当 VSPackage 请求环境更新当前用户界面 (UI)。 作为命令的当前用户可见的如将发生这种情况**剪切**，**副本**，并**粘贴**分组标准工具栏上，成为中启用和禁用对上下文和用户操作的响应。  
  
  由于 shell 托管了多个 Vspackage，shell 将令人无法接受会降低性能时所需轮询每个 VSPackage 来确定命令状态。 相反，你的 VSPackage，应主动通知环境更改时更改其 UI 时。 更新通知的详细信息，请参阅[更新用户界面](../../extensibility/updating-the-user-interface.md)。  
  
## <a name="status-notification-failure"></a>状态通知失败  
 你的 VSPackage 的失败通知命令状态已更改的环境可以将 UI 放在不一致的状态。 请记住，任何菜单或上下文菜单命令可以放置工具栏上的用户。 因此，仅当将打开一个菜单或上下文菜单时才更新 UI 是不够的。  
  
## <a name="see-also"></a>请参阅  
 [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [实现](../../extensibility/internals/command-implementation.md)
