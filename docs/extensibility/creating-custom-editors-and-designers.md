---
title: 创建自定义编辑器和设计器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0ddfe2b61c8ef08d77fbb7c841b3bb69c167af2f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903734"
---
# <a name="create-custom-editors-and-designers"></a>创建自定义编辑器和设计器

Visual Studio 集成开发环境 (IDE) 可托管不同类型的编辑器：

- Visual Studio 核心编辑器

- 自定义编辑器

- 外部编辑器

- 设计器

以下信息可帮助你选择所需编辑器的类型。

## <a name="types-of-editor"></a>编辑器类型

有关 Visual Studio 核心编辑器的信息，请参阅 [扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)。

### <a name="custom-editors"></a>自定义编辑器
 自定义编辑器是设计用于在专用环境中工作的编辑器。 例如，可以创建一个编辑器，该编辑器的函数将数据读写到特定存储库，如 Microsoft Exchange 服务器。 如果你希望编辑器仅适用于你的项目类型，或者需要仅具有几个特定命令的编辑器，请选择自定义编辑器。 但请注意，用户将无法使用自定义编辑器编辑标准 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目。

 自定义编辑器可以使用编辑器工厂，并将有关编辑器的信息添加到注册表中。 但是，与自定义编辑器关联的项目类型可以通过其他方式实例化自定义编辑器。

 自定义编辑器可以使用就地激活或简化的嵌入来实现视图。

### <a name="external-editors"></a>外部编辑器
 外部编辑器是未集成到 Visual Studio 中的编辑器，如 Microsoft Word、记事本或 Microsoft FrontPage。 例如，如果将文本传递到 VSPackage，则可以调用此类编辑器。 外部编辑器自行注册，可以在 Visual Studio 外部使用。 调用外部编辑器时，可以将其嵌入到主机窗口中，它将显示在 IDE 中的窗口中。 否则，IDE 将为其创建一个单独的窗口。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>方法使用枚举设置文档优先级 <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 。 如果 `DP_External` 指定了值，则可以通过外部编辑器打开该文件。

## <a name="editor-design-decisions"></a>编辑器设计决策
 以下设计问题将帮助你选择最适合你的应用程序的编辑器类型：

- 应用程序是否将其数据保存到文件中？ 如果它将数据保存在文件中，则它们将采用自定义还是标准格式？

   如果你使用标准文件格式，则除你的项目外，其他项目类型将能够对其打开和读/写数据。 但是，如果您使用自定义文件格式，则只有您的项目类型才能对其打开和读/写数据。

   如果你的项目使用文件，则应自定义标准编辑器。 如果你的项目不使用文件，而是使用数据库或其他存储库中的项，则应创建自定义编辑器。

- 您的编辑器是否需要承载 ActiveX 控件？

   如果编辑器承载 ActiveX 控件，则按 [就地激活](/visualstudio/misc/in-place-activation?view=vs-2015)中所述，实现就地激活编辑器。 如果它没有承载 ActiveX 控件，则使用简化的嵌入编辑器，或自定义 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 默认编辑器。

- 编辑器是否支持多个视图？ 如果希望编辑器的视图与默认编辑器同时可见，则必须支持多个视图。

   如果编辑器需要支持多个视图，则编辑器的文档数据和文档视图对象必须是单独的对象。 有关详细信息，请参阅 [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

   如果编辑器支持多个视图，是否打算为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 文档数据对象使用 (对象) 的核心编辑器文本缓冲区实现 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ？ 也就是说，您是否希望使用核心编辑器同时支持您的编辑器视图 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ？ 执行此操作的功能是窗体设计器的基础。

- 如果需要托管外部编辑器，是否可以在中嵌入编辑器 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ？

   如果可以嵌入，则应为外部编辑器创建宿主窗口，然后调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 方法，并将 <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 枚举值设置为 `DP_External` 。 如果编辑器无法嵌入，IDE 将自动为其创建一个单独的窗口。

## <a name="in-this-section"></a>本节内容

[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)\
说明如何创建自定义编辑器。

[演练：向自定义编辑器添加功能](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)\
说明如何将功能添加到自定义编辑器。

[设计器初始化和元数据配置](../extensibility/designer-initialization-and-metadata-configuration.md)\
说明如何初始化设计器。

[为设计器提供撤消支持](../extensibility/supplying-undo-support-to-designers.md)\
说明如何为设计器提供撤消支持。

[自定义编辑器中的语法着色](../extensibility/syntax-coloring-in-custom-editors.md)\
说明核心编辑器和自定义编辑器中语法着色之间的差异。

[自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)\
说明如何在自定义编辑器中实现文档数据和文档视图。

## <a name="related-sections"></a>相关章节

[编辑器中的旧接口](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)\
说明如何通过旧版 API 访问核心编辑器。

[开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)\
说明如何实现语言服务。

[扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)\
说明如何创建与的其余部分匹配的 UI 元素 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
