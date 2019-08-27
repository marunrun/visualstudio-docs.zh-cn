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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180300"
---
# <a name="language-services-and-the-core-editor"></a>语言服务和核心编辑器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中的编辑器经常与相关联的语言服务。 除此之外，语言服务都会提供语法着色、 语句完成、 IntelliSense 和文本格式设置。  
  
## <a name="core-editors-and-document-data-objects"></a>核心编辑器和文档数据对象  
 在访问核心编辑器时，您不要创建文档数据和文档视图对象。 IDE 创建和控制这两个对象，并通过工厂实现在编辑器中进行相应的调用获取指向它们的句柄。  
  
 有关详细信息，请参阅[在项目中确定哪个编辑器打开文件](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)。  
  
## <a name="language-services-and-the-core-editor"></a>语言服务和核心编辑器  
 通过实现语言服务时，可以控制数据在文档视图中的显示方式。 语言服务都会提供信息和特定于给定语言，如视觉对象的行为C++。 文本缓冲区时创建文本缓冲区，并确定要打开的文档的文件名扩展名，确定与从注册表项，HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Editors 此文件扩展名关联的语言服务\\{YourLanguageService GUID} \Extensions。 然后加载过程的标准 VSPackage 加载你的 VSPackage，并创建语言服务的实例。  
  
 基本语言服务是在下图中所示。  
  
 ![语言服务模型图](../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")  
核心编辑器和语言服务对象  
  
 核心编辑器文档数据对象称为文本缓冲区，由表示<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象。 文档视图对象称为文本视图，由表示<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>对象。 通过语言服务以提供核心编辑器的统一的视图，这两个对象一起工作。 文本缓冲区和文档窗口中显示的文本视图中的信息称为代码窗口。 代码窗口文档由代码窗口管理器管理。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 [使用旧版 API 提供的语言服务上下文](../extensibility/providing-a-language-service-context-by-using-the-legacy-api.md)   
 [IntelliSense 托管](../extensibility/intellisense-hosting.md)   
 [包含的语言](../extensibility/contained-languages.md)   
 [开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)
