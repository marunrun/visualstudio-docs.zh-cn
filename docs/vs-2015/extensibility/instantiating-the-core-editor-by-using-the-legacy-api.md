---
title: 实例化使用旧 API 的核心编辑器 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203914"
---
# <a name="instantiating-the-core-editor-by-using-the-legacy-api"></a>使用旧 API 实例化核心编辑器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在编辑器负责进行文本编辑功能，如插入、 删除、 复制和粘贴。 它将与所提供的语言服务，如文本颜色设置、 缩进和 IntelliSense 语句完成功能结合这些函数。  
  
 可以实例化三种方式之一中的核心编辑器的实例：  
  
- 显式创建的实例的核心编辑器在窗口中。  
  
- 提供一个编辑器工厂返回的核心编辑器实例  
  
- 从项目层次结构中打开一个文件。  
  
  以下部分介绍如何使用传统的 API 来实例化编辑器中。  
  
## <a name="explicitly-opening-a-core-editor-instance"></a>显式打开核心编辑器实例  
 当显式获取核心编辑器的实例：  
  
- 获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>以保存所编辑的文档数据对象。  
  
- 通过创建来创建面向行的文档数据对象表示形式<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>接口从<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>接口。  
  
- 设置<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>的文档数据对象的默认实现的实例作为<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>接口，使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow.SetBuffer%2A>方法。  
  
   主机<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>实例中<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>通过使用接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateToolWindow%2A>方法。  
  
  此时，显示<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>接口提供了一个窗口，其中包含核心编辑器的一个实例。  
  
  但是，这不是非常有用的实例，因为它不具有键盘快捷方式，或访问高级功能。 若要获取对键盘快捷方式和高级的功能的访问：  
  
- 使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>方法以将语言服务和编辑器使用的文档数据对象相关联。  
  
- 创建你自己键盘快捷方式，或通过设置使用系统默认<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>对象显示的属性。 若要执行此操作，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetGuidProperty%2A>方法替换<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>属性。  
  
   若要获得并使用非标准的快捷键，生成使用.vsct 文件。 有关详细信息，请参阅 [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。  
  
## <a name="how-to-use-an-editor-factory-to-obtain-the-core-editor"></a>如何使用编辑器工厂获取核心编辑器  
 实现与编辑器工厂使用的核心编辑器时<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法，请遵循所有用于显式托管在上一部分中所述的步骤<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>文档数据对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>对象。  
  
 若要显示的文本，获得<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口从<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>对象，并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法。  
  
 若要为编辑器提供语言服务，请调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>方法内的<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法。  
  
 若要获取默认键盘快捷方式，与上一节中，不同使用返回的命令上下文<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法获取从核心编辑器时<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法。  
  
 如果<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法返回相同的命令 GUID 的文本编辑器，核心编辑器的实例会自动获取默认键盘快捷方式。  
  
 有关常规信息，请参阅[演练：创建核心编辑器和注册编辑器文件类型](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)。  
  
## <a name="see-also"></a>请参阅  
 [在核心编辑器](../extensibility/inside-the-core-editor.md)   
 [打开和保存项目项](../extensibility/internals/opening-and-saving-project-items.md)   
 [演练：创建核心编辑器并注册编辑器文件类型](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)
