---
title: 语言服务和核心编辑器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - language services
ms.assetid: e03199a6-ad5f-4075-bfba-8d36865112b7
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1e708ffe796bfc9342bc20c3e7f20d5cf0d05058
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180300"
---
# <a name="language-services-and-the-core-editor"></a>语言服务和核心编辑器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 中的编辑器经常与语言服务相关联。 除此之外，语言服务还提供语法着色、语句完成、IntelliSense 和文本格式。  
  
## <a name="core-editors-and-document-data-objects"></a>核心编辑器和文档数据对象  
 访问核心编辑器时，不会创建文档数据和文档视图对象。 IDE 将创建并控制这两个对象，并通过在编辑器工厂实现中进行适当的调用来获取这些对象的句柄。  
  
 有关详细信息，请参阅 [确定哪个编辑器在项目中打开文件](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)。  
  
## <a name="language-services-and-the-core-editor"></a>语言服务和核心编辑器  
 通过实现语言服务，可以控制数据在文档视图中的显示方式。 语言服务提供特定于给定语言的信息和行为，如 Visual C++。 当你创建文本缓冲区并确定要打开的文档的文件扩展名时，文本缓冲区会从注册表项（HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Editors \\ {YOURLANGUAGESERVICE GUID} \Extensions.）确定与此文件扩展名关联的语言服务。 然后，标准 VSPackage 加载过程加载 VSPackage，并创建语言服务的实例。  
  
 下图显示了一个基本语言服务。  
  
 ![语言服务模型图](../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")  
核心编辑器和语言服务对象  
  
 核心编辑器的文档数据对象称为文本缓冲区，由 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 对象表示。 文档视图对象称为文本视图，由 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> 对象表示。 这两个对象通过语言服务协同工作，以提供核心编辑器的统一视图。 文本缓冲区和文本视图中的信息将显示在一个名为 "代码窗口" 的文档窗口中。 代码窗口文档由代码窗口管理器进行管理。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 [使用旧版 API 提供语言服务上下文](../extensibility/providing-a-language-service-context-by-using-the-legacy-api.md)   
 [IntelliSense 托管](../extensibility/intellisense-hosting.md)   
 [包含的语言](../extensibility/contained-languages.md)   
 [开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)
