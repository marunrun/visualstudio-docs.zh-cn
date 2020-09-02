---
title: 编辑器工厂 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - editor factories
ms.assetid: cf4e8164-3546-441d-b465-e8a836ae7216
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2de1fc8440bd33a526da62dbb4c7937800484aaa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197762"
---
# <a name="editor-factories"></a>编辑器工厂
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器工厂创建编辑器对象并将其放在称为 "物理视图" 的窗口框架中。 它创建创建编辑器和设计器所必需的文档数据和文档视图对象。 创建 Visual Studio 核心编辑器和任何标准编辑器时需要编辑器工厂。 还可以选择使用编辑器工厂创建自定义编辑器。  
  
 可以通过实现接口来创建编辑器工厂 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 。 下面的示例演示如何实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 以创建编辑器工厂：  
  
 [!code-csharp[VSSDKEditorFactories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkeditorfactories/cs/vssdkeditorfactoriespackage.cs#1)]
 [!code-vb[VSSDKEditorFactories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkeditorfactories/vb/vssdkeditorfactoriespackage.vb#1)]  
  
 首次打开由该编辑器处理的文件类型时，将加载编辑器。 您可以选择打开特定编辑器或默认编辑器。 如果选择默认编辑器，集成开发环境 (IDE) 确定要打开的正确编辑器，然后将其打开。 有关详细信息，请参阅 [确定哪个编辑器在项目中打开文件](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)。  
  
## <a name="registering-editor-factories"></a>注册编辑器工厂  
 在您可以使用您创建的编辑器之前，您首先必须注册有关该编辑器的信息，包括它可以处理的文件扩展名。  
  
 如果 VSPackage 是用托管代码编写的，则可以使用托管包框架 (MPF) 方法在 <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> 加载 VSPackage 后注册编辑器工厂。 如果 VSPackage 是用非托管代码编写的，则必须使用服务注册编辑器工厂 <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> 。  
  
### <a name="registering-an-editor-factory-by-using-managed-code"></a>使用托管代码注册编辑器工厂  
 你必须在 VSPackage 的方法中注册编辑器工厂 `Initialize` 。 第一次调用 `base.Initialize` ，然后调用 <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> 每个编辑器工厂  
  
 在托管代码中，无需取消注册编辑器工厂，因为 VSPackage 将为你处理此情况。 此外，如果你的编辑器工厂实现 <xref:System.IDisposable> ，它将在取消注册后自动释放。  
  
### <a name="registering-an-editor-factory-by-using-unmanaged-code"></a>使用非托管代码注册编辑器工厂  
 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 编辑器包的实现中，使用 `QueryService` 方法调用 `SVsRegisterEditors` 。 执行此操作将返回指向的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>通过传递接口的实现来调用方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 。 必须 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 在单独的类中 m) 。  
  
## <a name="the-editor-factory-registration-process"></a>编辑器工厂注册过程  
 当 Visual Studio 使用编辑器工厂加载编辑器时，将发生以下过程：  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]项目系统调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 。  
  
2. 此方法返回编辑器工厂。 但在项目系统实际需要编辑器之前，Visual Studio 会延迟加载编辑器的包。  
  
3. 当项目系统需要编辑器时，Visual Studio 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 一个专用方法，该方法返回文档视图和文档数据对象。  
  
4. 如果 Visual Studio 对编辑器工厂的调用使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 返回文档数据对象和文档视图对象，则 Visual studio 将创建文档窗口，将文档视图对象放入其中，并向运行的文档表中输入文档数据对象 (RDT) 。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>   
 [运行文档表](../extensibility/internals/running-document-table.md)
