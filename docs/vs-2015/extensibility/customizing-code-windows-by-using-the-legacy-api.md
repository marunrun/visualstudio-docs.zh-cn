---
title: 使用旧版 API 自定义代码窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - code windows
ms.assetid: 5328ab2f-55cb-4680-9744-ec79f55acd1b
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f15c649b8d857d2e920bb957e5975d296749cb86
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62556110"
---
# <a name="customizing-code-windows-by-using-the-legacy-api"></a>使用旧版 API 自定义代码窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

代码窗口是支持一个或多个文本视图的文档窗口对象。 代码窗口的确切功能取决于关联的语言服务。 在多文档界面 (MDI) 模式下，代码窗口是 MDI 子框架。  
  
 代码窗口由语言服务控制，每个语言服务都可以提供自己的代码窗口管理器。 这使语言服务能够向代码窗口添加自己的修饰，如波形曲线、着色等。 有关如何创建核心窗口的详细信息，请参阅 [使用旧 API 实例化核心编辑器](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)。  
  
 "代码" 窗口是一个 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 对象，该对象具有文本视图以及在对象中放置的任何修饰。 在核心编辑器的实例化过程中创建代码窗口时，语言服务可以将附加 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 到代码窗口，如下图所示。  
  
 ![CodeWindow 图](../extensibility/media/vscodewindow.gif "vscodewindow")  
代码窗口  
  
 语言服务实现代码窗口管理器，负责管理修饰，如下拉栏。 代码窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> 在代码窗口初始化过程中调用方法。 进行此调用时，语言服务可将下拉栏或按钮栏 (<xref:Microsoft.VisualStudio.TextManager.Interop.IVsButtonBarClient>) 添加到代码窗口。  
  
## <a name="in-this-section"></a>本节内容  
 `Customizing Code Windows by Using the Legacy API`  
 介绍如何使用旧版 API 自定义代码窗口。  
  
 [如何：在编辑器中承载另一个编辑器](../extensibility/how-to-host-an-editor-in-another-editor.md)  
 说明如何在编辑器窗口中承载另一个编辑器。  
  
 [如何：在编辑器失去焦点时触发事件](../extensibility/how-to-fire-events-when-the-editor-loses-focus.md)  
 说明如何将文档视图附加到文档数据对象。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 [使用旧版 API 实例化核心编辑器](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)   
 [使用旧版 API 访问文本视图](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)
