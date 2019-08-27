---
title: 创建自定义编辑器和设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
caps.latest.revision: 32
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dc94d11a5ed118f0133657ebf5b966623a199d64
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197406"
---
# <a name="creating-custom-editors-and-designers"></a>创建自定义编辑器和设计器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 集成的开发环境 (IDE) 可以托管不同类型的编辑器：  
  
- Visual Studio 核心编辑器  
  
- 自定义编辑器  
  
- 外部编辑器  
  
- 设计器  
  
  以下信息可帮助你选择的编辑器所需的类型。  
  
## <a name="types-of-editor"></a>类型的编辑器  
 有关 Visual Studio 核心编辑器的信息，请参阅[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)。  
  
##### <a name="custom-editors"></a>自定义编辑器  
 自定义编辑器是一个用于处理在特殊情况下。 例如，可以创建的编辑器的函数是读取和写入到特定的存储库，如 Microsoft Exchange server 的数据。 如果你想要一个编辑器，适用于仅您的项目类型，如果希望编辑器具有仅几个特定命令，请选择自定义编辑器。 但请注意，用户将无法使用自定义编辑器来编辑标准[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]项目。  
  
 自定义编辑器可以使用编辑器工厂，并向注册表添加关于编辑器的信息。 但是，与自定义编辑器关联的项目类型可以实例化中的其他方法的自定义编辑器。  
  
 自定义编辑器可以使用就地激活或简化嵌入实现视图。  
  
##### <a name="external-editors"></a>外部编辑器  
 外部编辑器是未集成到 Visual Studio 中，如 Microsoft Word、 记事本或 Microsoft FrontPage 的编辑器。 如果，例如，要传递文本到它从你的 VSPackage，您可能会调用此类编辑器。 外部编辑器自行注册，并可以在 Visual Studio 外。 当调用外部编辑器，并可嵌入在宿主窗口时，然后它显示在 IDE 中窗口。 如果没有，则 IDE 将为其创建一个单独的窗口。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>方法使用设置文档的优先级<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>枚举。 如果`DP_External`指定值时，可以通过外部编辑器打开文件。  
  
## <a name="editor-design-decisions"></a>编辑器设计决策  
 以下的设计问题将帮助您选择适合你的应用程序的最佳编辑器类型：  
  
- 将你的应用程序将其数据保存在文件中或不？ 如果它将在文件中保存其数据，它们将采用自定义或标准格式？  
  
     如果使用标准文件格式，除了你的项目的其他项目类型将能够打开并读取/写入数据到它们。 如果使用自定义文件格式，但是，您的项目类型将能够打开并读取/写入数据到它们。  
  
     如果你的项目使用的文件，然后应自定义的标准编辑器。 如果你的项目不使用文件，但而是使用数据库或其他存储库中的项，则应创建自定义编辑器。  
  
- 你的编辑器是否需要托管 ActiveX 控件？  
  
     如果你的编辑器承载 ActiveX 控件，则实现就地激活编辑器，如中所述[就地激活](../misc/in-place-activation.md)。 如果它不承载 ActiveX 控件，然后使用简化的嵌入编辑器中，或自定义[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]默认编辑器。  
  
- 将你的编辑器支持多个视图？ 如果想要的编辑器的默认编辑器时是可见的视图，必须支持多个视图。  
  
     如果你的编辑器需要支持多个视图，文档数据和编辑器的文档视图对象必须是单独的对象。 有关详细信息，请参阅[Supporting Multiple Document Views](../extensibility/supporting-multiple-document-views.md)。  
  
     如果编辑器支持多个视图，你是否打算使用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器的文本缓冲区实现 (<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象) 的文档数据对象？ 要在即支持将编辑器视图--与并行[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器？ 若要执行此操作的功能是窗体设计器的基础...  
  
- 如果需要用于托管外部编辑器，可在编辑器嵌入在[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]？  
  
     如果它可以嵌入，应为外部编辑器创建宿主窗口，然后调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>方法，设置<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>枚举值`DP_External`。 如果不能嵌入编辑器，则 IDE 将自动为其创建一个单独的窗口。  
  
## <a name="in-this-section"></a>本节内容  
 [演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)  
 说明如何创建自定义编辑器。  
  
 [演练：在自定义编辑器中添加功能](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)  
 介绍如何将功能添加到自定义编辑器。  
  
 [设计器初始化和元数据配置](../extensibility/designer-initialization-and-metadata-configuration.md)  
 介绍如何初始化设计器。  
  
 [向设计器提供撤消支持](../extensibility/supplying-undo-support-to-designers.md)  
 介绍如何为设计器提供撤消支持。  
  
 [自定义编辑器中的语法着色](../extensibility/syntax-coloring-in-custom-editors.md)  
 介绍了语法着色和自定义编辑器中核心编辑器之间的差异。  
  
 [自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)  
 介绍如何在自定义编辑器中实现文档数据和文档视图。  
  
## <a name="related-sections"></a>相关章节  
 [编辑器中的旧接口](../extensibility/legacy-interfaces-in-the-editor.md)  
 说明如何通过传统的 API 访问核心编辑器。  
  
 [开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)  
 介绍如何实现语言服务。  
  
 [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)  
 说明如何创建匹配的其余部分的 UI 元素[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
