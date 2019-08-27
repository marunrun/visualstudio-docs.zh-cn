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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63002662"
---
# <a name="adding-web-services-to-project-systems"></a>将 Web 服务添加到项目系统
一般情况下，XML Web services 是以编程方式的信息返回到项目系统使用 SOAP （简单对象访问协议） 协议的 URL 可寻址资源。 您可以通过使用 Web 服务集成到 VSPackage 项目系统<xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg2>接口。  
  
### <a name="to-add-a-web-service-to-your-project-system"></a>若要将 Web 服务添加到项目系统  
  
1. 调用`QueryService`有关<xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg2>接口通过<xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg>服务。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2.AddWebReferenceDlg%2A> 方法。 如果您传入`pDiscoverySession`作为参数`NULL`、 为您创建发现会话和会话缓存，这样就可供后续使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2>接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2.AddWebReferenceDlg%2A> 方法返回一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult2>。  
  
3. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult.AddWebReference%2A> 方法。 在自动化对象中传递为 Web 服务的引用文件夹作为`pUnkWebReferenceFolder`参数。 在 Visual Studio 环境然后会检查 Web 服务是否已存在。 如果不存在 Web 服务，该环境下载，并将 Web 服务添加到一个文件夹和子节点的文件夹的任何其他文件 （如.wsdl 文件）。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoverySession>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService>