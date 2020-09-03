---
title: 使用旧版 API 实例化核心编辑器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - instantiating editor
ms.assetid: dda23b18-96ef-43c6-b0dc-06d15cbe5cbb
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 29306a16390039c8ee6e424b81a5ff617e533ab4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203914"
---
# <a name="instantiating-the-core-editor-by-using-the-legacy-api"></a>使用旧 API 实例化核心编辑器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器负责文本编辑功能，如插入、删除、复制和粘贴。 它将这些函数与语言服务提供的函数（如文本着色、缩进和 IntelliSense 语句完成）组合在一起。  
  
 可以通过以下三种方式之一实例化核心编辑器的实例：  
  
- 在窗口中显式创建核心编辑器的实例。  
  
- 提供一个返回核心编辑器实例的编辑器工厂  
  
- 从项目层次结构中打开文件。  
  
  以下各节介绍如何使用旧版 API 来实例化编辑器。  
  
## <a name="explicitly-opening-a-core-editor-instance"></a>显式打开核心编辑器实例  
 显式获取核心编辑器的实例时：  
  
- 获取 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 以保存正在编辑的文档数据对象。  
  
- 通过从接口创建接口，为文档数据对象创建面向行的表示形式 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>使用方法，将设置为接口的默认实现的实例的文档数据对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow.SetBuffer%2A> 。  
  
   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>使用方法在接口中托管实例 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateToolWindow%2A> 。  
  
  此时，显示 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 接口会提供一个包含核心编辑器实例的窗口。  
  
  但是，这不是一个非常有用的实例，因为它没有快捷键或访问高级功能。 若要获取对快捷键和高级功能的访问权限：  
  
- 使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> 方法可将语言服务和编辑器使用的文档数据对象关联起来。  
  
- 可以创建自己的快捷键，也可以通过设置对象显示属性来使用系统默认值 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 。 为此，请 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetGuidProperty%2A> 通过属性调用方法 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> 。  
  
   若要获取和使用非标准快捷键，请使用 .vsct 文件生成它们。 有关详细信息，请参阅 [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。  
  
## <a name="how-to-use-an-editor-factory-to-obtain-the-core-editor"></a>如何使用编辑器工厂获取核心编辑器  
 使用方法通过编辑器工厂实现核心编辑器时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ，请按照上一节中所述的所有步骤， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> 在对象中显式承载使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 文档数据对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 。  
  
 若要显示文本，请 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 从对象获取接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> 并调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 方法。  
  
 若要向编辑器提供语言服务，请 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> 在方法中调用方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 。  
  
 若要获取默认快捷键，与上一节不同，请在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 从方法获取核心编辑器时使用方法返回的命令上下文 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 。  
  
 如果该 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 方法返回与文本编辑器相同的命令 GUID，则核心编辑器的实例会自动获取默认快捷键。  
  
 有关一般信息，请参阅 [演练：创建核心编辑器和注册编辑器文件类型](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在核心编辑器内](../extensibility/inside-the-core-editor.md)   
 [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)   
 [演练：创建核心编辑器并注册编辑器文件类型](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)
