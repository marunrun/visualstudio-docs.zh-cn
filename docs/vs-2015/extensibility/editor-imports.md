---
title: 编辑器导入 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - services
ms.assetid: 8d096de3-33b4-427a-a122-4aeff8a72da0
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1fc32d0126d912acab104ecefe3cb62d80b8513f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690320"
---
# <a name="editor-imports"></a>编辑器导入
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以导入多个编辑器服务、工厂和代理，它们为你的扩展提供对核心编辑器的不同类型的访问。 例如，你可以导入， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 以便为你提供 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> 给定内容类型的。  (此导航器可对文本缓冲区执行不同种类的搜索。 )   
  
 若要使用编辑器导入，请将其作为导出 Managed Extensibility Framework 组件部分的类的字段或属性导入。  
  
> [!NOTE]
> 有关 Managed Extensibility Framework 的详细信息，请参阅 [Managed Extensibility Framework (MEF) ](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)。  
  
## <a name="import-syntax"></a>Import 语法  
 下面的示例演示如何导入编辑器选项工厂服务。  
  
```  
[Import]  
internal IEditorOptionsFactoryService EditorOptions { get; set; }  
```  
  
 如果要将服务作为字段而不是属性导入，则应在声明中将其设置为， `null` 以避免编译器有关不赋值给变量的警告：  
  
```  
[Import]  
internal IEditorOptionsFactoryService m_editorOptions = null;  
```  
  
 有关使用导入的更多示例，请参阅以下演练：  
  
 [演练：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)  
  
 [演练：自定义文本视图](../extensibility/walkthrough-customizing-the-text-view.md)  
  
 [演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)  
  
 [演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)  
  
 [演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)  
  
 [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)  
  
 [演练：显示智能标记](../misc/walkthrough-displaying-smarttags.md)  
  
## <a name="importing-the-service-provider"></a>导入服务提供程序  
 您还可以导入 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> 在 VisualStudio) 中找到的 (，以获取对 Visual Studio 服务的访问权限：  
  
```  
[Import]  
internal SVsServiceProvider ServiceProvider = null;   
```  
  
 有关详细信息，请参阅 [演练：从编辑器扩展访问 DTE 对象](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md) 。  
  
## <a name="services"></a>服务  
 编辑器服务通常是单个实体，提供服务并在多个组件之间共享。  
  
|导入|提供|  
|------------|--------------|  
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|文件扩展名和对象之间的关系 <xref:Microsoft.VisualStudio.Utilities.IContentType> 。|  
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|<xref:Microsoft.VisualStudio.Utilities.IContentType> 对象的集合。|  
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation>对象|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|许多编辑器适配器对象：<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|  
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch>给定文本视图的对象。|  
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|  
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextDocument>。|  
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601>差异的。|  
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection>差异的。|  
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>或 <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer> 。|  
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>一组 <xref:Microsoft.VisualStudio.Text.ITextBuffer> 对象的。|  
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> <xref:Microsoft.VisualStudio.Text.ITextBuffer> 。|  
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|的 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|维护对象的集合 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> 。|  
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>文本缓冲区的。|  
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>文本视图的。|  
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions>指定范围的。|  
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMap>文本视图的。|  
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|的 <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|通过对象获取自动缩进 <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider> 。|  
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|管理的 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> 。|  
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>。|  
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|从一组快照范围生成 RTF 格式的文本。|  
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer>的 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|<xref:System.Windows.Media.TextFormatting.TextParagraphProperties>用于设置视图中的文本行格式的。|  
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|的 <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations> 对象 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|搜索文本快照。|  
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> <xref:Microsoft.VisualStudio.Text.ITextBuffer> 由的 <xref:Microsoft.VisualStudio.Utilities.IContentType> 。|  
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>文本视图的。|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|一组标准字形。|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|的 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|跟踪键盘处理。|  
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|标准 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> 对象。|  
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|维护文本缓冲区和对象之间的关系  <xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory> 。|  
  
## <a name="other-imports"></a>其他导入  
 提供程序工厂和代理通常是可在多个组件中具有多个实例的实体。  
  
|导入|提供|  
|------------|--------------|  
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|<xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> 给定缓冲区的类型) 的。|  
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|文本标记标记 (<xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> 类型 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>) 的。|  
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider>给定的 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>。|  
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>。|  
  
## <a name="see-also"></a>另请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
