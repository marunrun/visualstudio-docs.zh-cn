---
title: 互通程序集中的命令协定 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command handling with interop assemblies, command contracts
- interop assemblies, command contracts
ms.assetid: 57245708-f539-42dc-8963-2754a48f0189
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4f20a4f479d62cd1b64c3b13ff6e1a949656a668
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709686"
---
# <a name="command-contracts-in-interop-assemblies"></a>互通程序集中的命令协定
通过<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口处理命令的基本协定是，环境调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法以确定该命令是否受支持，如果支持该命令，则确定其状态和文本。 然后，环境调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法执行命令。

 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>该方法对所有命令的处理方式相同。 如果需要，通过使用适当的参数调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>方法来管理进一步的通信（例如，使用下拉列表）。 这些参数的解释取决于指定的命令。

 如果命令目标返回输出参数中的值，则调用方始终负责释放已分配的任何资源。 由于此参数是变体，因此清除变体将释放资源。

 如果命令必须在层次结构窗口中运行，<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>则必须使用接口。 接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>具有类似的协定，其方法相似：<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>。

## <a name="see-also"></a>请参阅
- [VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VS 包中的命令路由](../../extensibility/internals/command-routing-in-vspackages.md)
- [命令实现](../../extensibility/internals/command-implementation.md)
