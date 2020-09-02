---
title: 将 Web 服务添加到项目系统 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- project systems, adding Web services
- Web services, adding to VSPackage project systems
ms.assetid: 8efa078b-68b2-45a2-9be2-44f807bc0d7f
caps.latest.revision: 8
manager: jillfra
ms.openlocfilehash: f5b192be8e5f68ad9314fe08fff963c032013cb0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "63002662"
---
# <a name="adding-web-services-to-project-systems"></a>将 Web 服务添加到项目系统
XML Web 服务通常是 URL 可寻址的资源，它使用 SOAP (简单对象访问协议) 协议将编程信息返回到项目系统。 你可以使用接口将 Web 服务集成到你的 VSPackage 项目系统 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg2> 。  
  
### <a name="to-add-a-web-service-to-your-project-system"></a>将 Web 服务添加到项目系统  
  
1. `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg2> 通过服务调用接口 <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2.AddWebReferenceDlg%2A> 方法。 如果以参数的 `pDiscoverySession` 形式传递 `NULL` ，则会为你创建发现会话，并缓存该会话，以便它可供 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2> 接口使用。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2.AddWebReferenceDlg%2A> 方法返回指向的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult2> 。  
  
3. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult.AddWebReference%2A> 方法。 传入作为参数的 Web 服务引用文件夹的自动化对象 `pUnkWebReferenceFolder` 。 然后，Visual Studio 环境会检查 Web 服务是否已存在。 如果 Web 服务不存在，则环境会将 Web 服务下载并添加到文件夹中，并将任何其他文件 (例如 .wsdl 文件) 到文件夹的子节点。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoverySession>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService>