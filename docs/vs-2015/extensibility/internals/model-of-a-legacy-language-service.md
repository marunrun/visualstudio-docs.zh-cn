---
title: 旧版语言服务模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 27d51df6dd11509b86e6648d59978b87d9cd8a02
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157653"
---
# <a name="model-of-a-legacy-language-service"></a>旧版语言服务模型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

语言服务定义的元素和特定语言的功能，用于在编辑器提供特定于该语言的信息。 例如，在编辑器需要知道的元素和语言的关键字，才能支持语法突出显示。  
  
 语言服务由编辑器和包含编辑器中的视图的文本缓冲区与紧密合作。 Microsoft IntelliSense**快速信息**选项是通过语言服务提供一项功能的示例。  
  
## <a name="a-minimal-language-service"></a>最小语言服务  
 最基本的语言服务包含以下两个对象：  
  
- *语言服务*实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口。 语言服务包含的语言，包括其名称、 文件扩展名，代码窗口管理器中和着色器有关的信息。  
  
- *Colorizer*实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>接口。  
  
  以下概念图显示了一个模型的基本语言服务。  
  
  ![语言服务模型图](../../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")  
  基本语言服务模型  
  
  文档窗口承载*文档视图*编辑器中，在此情况下的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]核心编辑器。 文档视图和文本缓冲区拥有通过在编辑器中。 这些对象使用[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]通过专用的文档窗口称为*代码窗口*。 中包含代码窗口<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>对象是创建和控制的 IDE。  
  
  加载给定扩展名的文件时，编辑器查找与该扩展插件关联的语言服务并将传递给它的代码窗口通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>方法。 此语言服务将返回*代码窗口管理器*，它可以实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>接口。  
  
  下表概述了在模型中的对象。  
  
|组件|对象|函数|  
|---------------|------------|--------------|  
|文本缓冲区|<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>|Unicode 读取/写入文本流。 很可能要使用其他编码文本。|  
|“代码”窗口|<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>|包含一个或多个文本视图的文档窗口。 当[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]是在多文档界面 (MDI) 模式下，代码窗口是 MDI 子窗体。|  
|文本视图|<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>|允许用户导航并通过使用键盘和鼠标来查看文本窗口。 文本视图作为一个编辑器，显示给用户。 您可以使用普通的编辑器窗口、 输出窗口和即时窗口中的文本视图。 此外，还可以配置代码窗口中的一个或多个文本视图。|  
|文本管理器|由管理<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>服务，从其获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager>指针|维护由前面所述的所有组件共享的常见信息组件。|  
|语言服务|实现取决于;实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>|为编辑器提供了特定于语言的信息，如语法突出显示、 语句完成和大括号匹配的对象。|  
  
## <a name="see-also"></a>请参阅  
 [自定义编辑器中的文档数据和文档视图](../../extensibility/document-data-and-document-view-in-custom-editors.md)
