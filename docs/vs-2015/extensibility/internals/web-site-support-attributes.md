---
title: 网站支持属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 75401eb0d5acd5d363d05aec57909eef5b9855e3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68144301"
---
# <a name="web-site-support-attributes"></a>网站支持属性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 网站项目可以扩展以提供对 Web 编程语言的支持。 语言必须自行注册， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 以便在选择该语言时，项目模板可以出现在 " **新建** 网站" 对话框中。  
  
 IronPython Studio 示例包括网站支持。 可以在 [VSSDK 示例](../../misc/vssdk-samples.md)中找到它。 它包括以下属性类，以便将 IronPython 注册为新 Web 项目的代码隐藏语言。  
  
## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute  
 此属性放置在语言项目上。 它将语言添加到 "**新建**网站" 对话框的 "**语言**" 列表中的 Web 编程语言列表。 例如，以下内容将 IronPython 添加到列表中：  
  
```  
[WebSiteProject("IronPython", "Iron Python")]public class PythonProjectPackage : ProjectPackage  
```  
  
 此属性还将模板路径设置为指向 "模板" 文件夹。 有关模板文件夹位置的详细信息，请参阅网站 [支持模板](../../extensibility/internals/web-site-support-templates.md)。  
  
## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute  
 此属性放置在语言项目上。 它允许网站项目将一种文件类型（ (相关) ）嵌套在 **解决方案资源管理器**中 (主) 的另一文件类型下。  
  
 例如：  
  
```  
[WebSiteProjectRelatedFiles("aspx", "py")]public class PythonProjectPackage : ProjectPackage  
```  
  
 指定 IronPython 代码隐藏文件与 .aspx 文件相关。 在 IronPython 网站解决方案中创建新的 .aspx 网页时，将生成一个新的 py 源文件，并将其显示为 .aspx 页面的子节点。  
  
## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute  
 此属性位于语言项目包上。 它选择语言的 Intellisense 提供程序。  
  
 例如：  
  
```  
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]public class PythonPackage : Package, IOleComponent  
```  
  
 指定应根据需要创建一个 PythonIntellisenseProvider 实例， <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> 以提供语言服务。  
  
 当请求带有代码但未缓存的网页时，IVsIntellisenseProject 实现将处理引用并调用语言编译器。  
  
## <a name="see-also"></a>另请参阅  
 [网站支持](../../extensibility/internals/web-site-support.md)
