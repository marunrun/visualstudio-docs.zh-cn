---
title: 编辑器导入 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - services
ms.assetid: 8d096de3-33b4-427a-a122-4aeff8a72da0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6af95b452166aa71950ac1e869d333d12d857b9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712015"
---
# <a name="editor-imports"></a>编辑器导入
您可以导入许多编辑器服务、工厂和代理，这些服务、工厂和代理为您的扩展提供对核心编辑器的不同类型的访问权限。 例如，可以导入<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>以为您提供给定内容类型的 。 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> （此导航器允许您在文本缓冲区上执行不同类型的搜索。

 要使用编辑器导入，可以将其导入为导出托管扩展框架组件部分的类的字段或属性。

> [!NOTE]
> 有关托管扩展性框架的详细信息，请参阅[托管扩展性框架 （MEF）。](/dotnet/framework/mef/index)

## <a name="import-syntax"></a>导入语法
 下面的示例演示如何导入编辑器选项工厂服务。

```
[Import]
internal IEditorOptionsFactoryService EditorOptions { get; set; }
```

 如果要将服务导入为字段而不是属性，则应`null`在声明中将其设置为，以避免编译器警告不要分配给变量：

```
[Import]
internal IEditorOptionsFactoryService m_editorOptions = null;
```

 有关使用导入的更多示例，请参阅以下演练：

- [演练：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)

- [演练：自定义文本视图](../extensibility/walkthrough-customizing-the-text-view.md)

- [演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)

- [演练：显示快速信息工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)

- [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)

- [演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)

## <a name="import-the-service-provider"></a>导入服务提供商
 您还可以以相同的方式导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>（在程序集 Microsoft.VisualStudio.Shell.Immutable.10.0） 访问 Visual Studio 服务：

```csharp
[Import]
internal SVsServiceProvider ServiceProvider = null;
```

 有关详细信息[，请参阅演练：从编辑器扩展访问 DTE 对象](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md)。

## <a name="services"></a>服务
 编辑器服务通常是单个实体，提供服务并在多个组件之间共享。

|导入|提供|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|文件扩展名和<xref:Microsoft.VisualStudio.Utilities.IContentType>对象之间的关系。|
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|<xref:Microsoft.VisualStudio.Utilities.IContentType> 对象的集合。|
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation>对象。|
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|许多编辑器适配器对象：<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|给定<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch>文本视图的对象。|
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|一个<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|一个<xref:Microsoft.VisualStudio.Text.ITextDocument>。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|一<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601>种差异。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|一<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection>种差异。|
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|或<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer> <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer>。|
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|一<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>组对象。 <xref:Microsoft.VisualStudio.Text.ITextBuffer>|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|的<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>。 <xref:Microsoft.VisualStudio.Text.ITextBuffer>|
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|的<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|的<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>|
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|的<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap>。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|维护<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>对象的集合。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|文本<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>缓冲区的 。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|文本<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>视图的 。|
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|指定<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions>作用域的 的 。|
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|文本<xref:Microsoft.VisualStudio.Text.Editor.IScrollMap>视图的 。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|的<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent>。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|通过<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider>对象获取自动缩进。|
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|管理<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>的<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|一个<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|从一组快照范围生成 RTF 格式的文本。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|的<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer>。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|用于<xref:System.Windows.Media.TextFormatting.TextParagraphProperties>设置视图中的文本行的格式。|
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations>的对象<xref:Microsoft.VisualStudio.Text.Editor.ITextView>。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|搜索文本快照。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|a <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> <xref:Microsoft.VisualStudio.Text.ITextBuffer> for <xref:Microsoft.VisualStudio.Utilities.IContentType>by 。|
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|文本<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>视图的 。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|一组标准的字形。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|的<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack>。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|跟踪键盘处理。|
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|标准<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>对象。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|维护文本缓冲区和<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory>对象之间的关系。|

## <a name="other-imports"></a>其他进口
 提供程序工厂和代理通常是多个组件中可以有多个实例的实体。

|导入|提供|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|<xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601>给定缓冲区的类型<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>。|
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|文本标记标记器（类型一<xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601><xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>个 ）。|
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|给定<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider> <xref:Microsoft.VisualStudio.Text.Editor.ITextView>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|一个<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|一个<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|一个<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>。|

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
