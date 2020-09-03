---
title: VSPackage 结构 (源代码管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 08bb0a296daca0de1c02b905a75fb10ce05f254e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205995"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 结构（源代码管理 VSPackage）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

源代码管理包 SDK 提供了创建 VSPackage 的指导原则，使源代码管理实施者能够将其源代码管理功能与 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 环境集成。 VSPackage 是一种 COM 组件，通常由 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 集成开发环境按需加载 (IDE) 基于其注册表项中由包播发的服务。 每个 VSPackage 都必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 。 VSPackage 通常使用 IDE 提供的服务 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，并提供自己的某些服务。  
  
 VSPackage 声明其菜单项，并通过 .vsct 文件建立默认项状态。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE 将在此状态下显示菜单项，直到加载了 VSPackage。 然后，调用方法的 VSPackage 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 来启用或禁用菜单项。  
  
## <a name="source-control-package-characteristics"></a>源代码管理包特性  
 源代码管理 VSPackage 已深度集成到中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 VSPackage 语义包括：  
  
- 要实现的接口是接口的 VSPackage (`IVsPackage`)   
  
- UI 命令实现 ( 的接口的 .vsct 文件和实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>)   
  
- 将 VSPackage 注册到 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
  源代码管理 VSPackage 必须与以下其他实体通信 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ：  
  
- 项目  
  
- 编辑器  
  
- 解决方案  
  
- Windows  
  
- 正在运行的文档表  
  
### <a name="visual-studio-environment-services-that-may-be-consumed"></a>可能使用的 Visual Studio 环境服务  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 SVsRegisterScciProvider 服务  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>  
  
### <a name="vsip-interfaces-implemented-and-called"></a>已实现并调用 VSIP 接口  
 源代码管理包是一个 VSPackage，因此它可以与向注册的其他 Vspackage 直接交互 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 为了提供完整的源代码管理功能，源代码管理 VSPackage 可以处理项目或 shell 所提供的接口。  
  
 中的每个项目 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 都必须实现， <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> 才能被识别为 IDE 中的项目 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 但是，此接口专用于源代码管理。 预期受源代码管理的项目将实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> 。 源代码管理 VSPackage 使用此接口来查询项目的内容，并提供 it 标志符号和绑定信息 (在服务器位置与受源代码管理) 的项目的磁盘位置之间建立连接所需的信息。  
  
 源代码管理 VSPackage 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> ，后者又允许项目自行注册源代码管理，并检索其状态字形。  
  
 有关源代码管理 VSPackage 必须考虑的接口的完整列表，请参阅 [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)   
 [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
