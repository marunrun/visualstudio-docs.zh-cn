---
title: 互操作程序集中的命令协定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- command handling with interop assemblies, command contracts
- interop assemblies, command contracts
ms.assetid: 57245708-f539-42dc-8963-2754a48f0189
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 50d48d3a8ff55559cce1c3a40142e31b8eebd85f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195121"
---
# <a name="command-contracts-in-interop-assemblies"></a>互操作程序集中的命令协定
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

通过接口处理命令的基本协定 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 是，环境调用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法来确定命令是否受支持，如果受支持，则确定其状态和文本。 然后，环境调用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法来执行命令。  
  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>对于所有命令，此方法的处理方式相同。 如果需要，还需要进行进一步的通信 (例如，使用下拉列表) ，可通过 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 使用适当的参数调用方法来进行管理。 这些参数的解释取决于指定的命令。  
  
 如果命令目标返回 output 参数中的值，则调用方始终负责释放已分配的所有资源。 由于此参数是一个变量，因此清除变量将释放资源。  
  
 如果命令必须在层次结构窗口中运行，则 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 必须使用接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口具有具有类似方法的类似协定： <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> 。  
  
## <a name="see-also"></a>另请参阅  
 [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Vspackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)   
 [实现](../../extensibility/internals/command-implementation.md)
