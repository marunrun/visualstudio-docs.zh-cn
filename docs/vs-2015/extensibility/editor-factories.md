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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197762"
---
# <a name="editor-factories"></a>编辑器工厂
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器工厂创建编辑器对象，并将其放在窗口框架中，称为物理视图。 它创建的文档数据和创建编辑器和设计器所需的文档视图对象。 创建 Visual Studio 核心编辑器和任何标准编辑器需要编辑器工厂。 也可以使用编辑器工厂创建的自定义编辑器。  
  
 通过实现创建编辑器工厂<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口。 下面的示例演示如何实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>创建编辑器工厂：  
  
 [!code-csharp[VSSDKEditorFactories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkeditorfactories/cs/vssdkeditorfactoriespackage.cs#1)]
 [!code-vb[VSSDKEditorFactories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkeditorfactories/vb/vssdkeditorfactoriespackage.vb#1)]  
  
 编辑器是加载第一次打开该编辑器所处理的文件类型。 您可以选择打开特定的编辑器或默认编辑器。 如果您选择的默认编辑器，在集成的开发环境 (IDE) 确定正确的编辑器打开，然后打开它。 有关详细信息，请参阅[在项目中确定哪个编辑器打开文件](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)。  
  
## <a name="registering-editor-factories"></a>注册编辑器工厂  
 可以使用一种编辑器，已创建之前，首先必须注册信息，包括它可以处理的文件扩展名。  
  
 如果你的 VSPackage 用托管代码编写的您可以使用托管包框架 (MPF) 方法<xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A>后加载你的 VSPackage 注册编辑器工厂。 如果你的 VSPackage 编写在非托管代码中，则必须使用注册编辑器工厂<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors>服务。  
  
### <a name="registering-an-editor-factory-by-using-managed-code"></a>使用注册编辑器工厂的托管代码  
 必须在你的 VSPackage 中注册你的编辑器工厂`Initialize`方法。 第一次调用`base.Initialize`，然后调用<xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A>为每个编辑器工厂  
  
 在托管代码中没有无需取消注册一个编辑器工厂，因为 VSPackage 将为你处理此。 此外，如果您的编辑器工厂实现<xref:System.IDisposable>，取消注册时自动释放。  
  
### <a name="registering-an-editor-factory-by-using-unmanaged-code"></a>使用非托管的代码注册编辑器工厂  
 在中<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>编辑器包，使用实现`QueryService`方法来调用`SVsRegisterEditors`。 执行此操作将返回一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors>。 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>方法并传递的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口。 必须 mplement<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>在单独的类。  
  
## <a name="the-editor-factory-registration-process"></a>编辑器工厂注册过程  
 Visual Studio 加载使用编辑器工厂编辑器时，将发生以下过程：  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]项目系统调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>。  
  
2. 此方法返回编辑器工厂。 Visual Studio 而延迟加载编辑器的包，但是，直到项目系统实际上需要在编辑器。  
  
3. 当项目系统需要在编辑器时，Visual Studio 会调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>，返回的文档视图和文档数据对象的专用的方法。  
  
4. 如果编辑器工厂使用由 Visual Studio 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>返回文档数据对象，文档视图对象中，Visual Studio 文档窗口、 置于文档视图对象，然后创建到正在运行文档中的一个条目文档数据对象表 (RDT)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>   
 [运行文档表](../extensibility/internals/running-document-table.md)
