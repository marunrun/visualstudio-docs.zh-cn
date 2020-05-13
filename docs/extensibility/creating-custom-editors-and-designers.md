---
title: 创建自定义编辑器和设计师 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b9f56b82225e1e40782b6753bea03d3c1780f596
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739485"
---
# <a name="create-custom-editors-and-designers"></a>创建自定义编辑器和设计器

Visual Studio 集成开发环境 （IDE） 可以承载不同类型的编辑器：

- 视觉工作室核心编辑器

- 自定义编辑器

- 外部编辑器

- 设计器

以下信息可帮助您选择所需的编辑器类型。

## <a name="types-of-editor"></a>编辑器的类型

有关 Visual Studio 核心编辑器的信息，请参阅[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)。

### <a name="custom-editors"></a>自定义编辑器
 自定义编辑器是专为在特殊情况下工作而设计的编辑器。 例如，您可以创建一个编辑器，其功能是将数据读取和写入特定存储库（如 Microsoft Exchange 服务器）。 如果希望编辑器仅与项目类型配合使用，或者希望编辑器仅具有几个特定命令，请选择自定义编辑器。 但是请注意，用户将无法使用自定义编辑器编辑标准[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]项目。

 自定义编辑器可以使用编辑器工厂，并将有关编辑器的信息添加到注册表中。 但是，与自定义编辑器关联的项目类型可以以其他方式实例化自定义编辑器。

 自定义编辑器可以使用就地激活或简化嵌入来实现视图。

### <a name="external-editors"></a>外部编辑器
 外部编辑器是未集成到可视化工作室的编辑，例如 Microsoft Word、记事本或 Microsoft FrontPage。 例如，如果您从 VSPackage 向该编辑器传递文本，则可以调用此类编辑器。 外部编辑器自行注册，可在可视化工作室外使用。 当您调用外部编辑器时，它可以嵌入到主机窗口中，然后它将显示在 IDE 窗口中。 如果没有，则 IDE 会为其创建单独的窗口。

 该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>使用<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>枚举设置文档优先级。 如果指定`DP_External`了该值，则外部编辑器可以打开该文件。

## <a name="editor-design-decisions"></a>编辑器设计决策
 以下设计问题将帮助您选择最适合您的应用程序的编辑器类型：

- 您的应用程序是否会将其数据保存在文件中？ 如果它将数据保存在文件中，它们是否采用自定义格式或标准格式？

   如果使用标准文件格式，除了项目之外的其他项目类型将能够打开和读取/写入数据。 但是，如果您使用自定义文件格式，则只有项目类型才能打开和读取/写入数据。

   如果项目使用文件，则应自定义标准编辑器。 如果项目不使用文件，而是使用数据库或其他存储库中的项目，则应创建自定义编辑器。

- 编辑器是否需要托管 ActiveX 控件？

   如果编辑器承载 ActiveX 控件，则实现就地激活编辑器，如[就地激活](/visualstudio/misc/in-place-activation?view=vs-2015)中所述。 如果它不承载 ActiveX 控件，则使用简化的嵌入编辑器或自定义[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]默认编辑器。

- 您的编辑会支持多个视图吗？ 如果希望编辑器的视图与默认编辑器同时可见，则必须支持多个视图。

   如果编辑器需要支持多个视图，则编辑器的文档数据和文档视图对象必须是单独的对象。 有关详细信息，请参阅[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

   如果编辑器支持多个视图，您是否计划对文档数据对象使用[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]核心编辑器的文本缓冲区实现（<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象）？ 也就是说，是否要支持编辑器与[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]核心编辑器并排查看？ 执行此操作的能力是表单设计器的基础。

- 如果需要托管外部编辑器，编辑器是否可以嵌入到内部[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]？

   如果可以嵌入它，则应为外部编辑器创建一个主机窗口，<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>然后调用 方法并将枚举值设置为<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>`DP_External`。 如果无法嵌入编辑器，IDE 将自动为其创建单独的窗口。

## <a name="in-this-section"></a>本节内容

[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)\
说明如何创建自定义编辑器。

[演练：向自定义编辑器添加功能](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)\
说明如何向自定义编辑器添加功能。

[设计器初始化和元数据配置](../extensibility/designer-initialization-and-metadata-configuration.md)\
说明如何初始化设计器。

[向设计人员提供撤消支持](../extensibility/supplying-undo-support-to-designers.md)\
说明如何为设计人员提供撤消支持。

[自定义编辑器中的语法着色](../extensibility/syntax-coloring-in-custom-editors.md)\
解释核心编辑器和自定义编辑器中的语法着色之间的区别。

[自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)\
说明如何在自定义编辑器中实现文档数据和文档视图。

## <a name="related-sections"></a>相关章节

[编辑器中的旧接口](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)\
说明如何通过旧 API 访问核心编辑器。

[开发传统语言服务](../extensibility/internals/developing-a-legacy-language-service.md)\
说明如何实现语言服务。

[扩展视觉工作室的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)\
说明如何创建与 的其余部分匹配的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]UI 元素。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
