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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205995"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 结构（源代码管理 VSPackage）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

源控件包 SDK 提供了用于创建 VSPackage 的准则允许源控件实施者，将使用其自己的源代码管理功能进行集成[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]环境。 VSPackage 是 COM 组件，通常按需加载[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成的开发环境 (IDE) 基于由其注册表项中的包播发的服务。 每个 VSPackage 必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>。 VSPackage 通常使用所提供的服务[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE 和提供某些服务。  
  
 VSPackage 声明其菜单项，并建立通过.vsct 文件的默认项状态。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE 将加载 VSPackage 之前在此状态中显示的菜单项。 随后，VSPackage 的实现的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>调用方法来启用或禁用菜单项。  
  
## <a name="source-control-package-characteristics"></a>源控件的封装特性  
 源代码管理 VSPackage 紧密地集成到[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 VSPackage 语义包括：  
  
- 由于正在 VSPackage 实现的接口 (`IVsPackage`接口)  
  
- UI 命令实现 (.vsct 文件和实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口)  
  
- 使用 VSPackage 注册[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
  源代码管理 VSPackage 必须与通信这些其他[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]实体：  
  
- 项目  
  
- 编辑器  
  
- 解决方案  
  
- Windows  
  
- 运行文档表  
  
### <a name="visual-studio-environment-services-that-may-be-consumed"></a>可能使用的 visual Studio 环境服务  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 SVsRegisterScciProvider 服务  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>  
  
### <a name="vsip-interfaces-implemented-and-called"></a>VSIP 接口实现和调用  
 源代码管理包是 VSPackage，并因此它可直接与注册的其他 Vspackage 交互[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 为了提供全套的源代码管理功能，源代码管理 VSPackage 可以处理提供的项目或 shell 接口。  
  
 每个项目中的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>若要识别为中的项目[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE。 但是，此接口不专用足够用于源代码管理。 应为源下的项目控件实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>。 若要查询对其内容的项目，并将该标志符号和绑定信息 （所需的信息的服务器位置和下一个项目的磁盘位置之间建立连接，使用此接口由源代码管理 VSPackage源代码管理）。  
  
 源代码管理 VSPackage 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>，这反过来允许项目进行源代码管理中注册自身和检索其状态的标志符号。  
  
 源代码管理 VSPackage 必须考虑的接口的完整列表，请参阅[相关服务和界面](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)。  
  
## <a name="see-also"></a>请参阅  
 [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)   
 [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
