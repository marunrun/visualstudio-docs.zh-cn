---
title: 语言服务和编辑器扩展点 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extension points
ms.assetid: 91a6417e-a6fe-4bc2-9d9f-5173c634a99b
caps.latest.revision: 34
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5bf0e34c76406b054ea2d27434f749b676b0b30c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439801"
---
# <a name="language-service-and-editor-extension-points"></a>语言服务和编辑器扩展点
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

该编辑器还提供可以扩展为 Managed Extensibility Framework (MEF) 组件部件，其中包括大多数语言服务功能的扩展点。 主要扩展点类别如下：  
  
- 内容类型  
  
- 分类类型和分类格式  
  
- 边距和滚动条  
  
- Tags  
  
- 修饰  
  
- 鼠标处理器  
  
- 拖放处理程序  
  
- 选项  
  
- IntelliSense  
  
## <a name="extending-content-types"></a>扩展内容类型  
 内容类型是类型的文本编辑器，例如处理、"text"、"代码"或"CSharp"的定义。 通过声明类型的变量来定义新的内容类型<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>并提供一个唯一的名称的新内容类型。 若要使用编辑器注册内容类型，请将其导出以及以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 是的内容类型的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute> 是从中派生此内容类型的内容类型的名称。 内容类型可以从多个其他内容类型继承。  
  
  因为<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>类密封的可以将其导出不使用任何类型参数。  
  
  下面的示例演示的内容类型定义导出特性。  
  
```  
[Export]  
[Name("test")]  
[BaseDefinition("code")]  
[BaseDefinition("projection")]  
internal static ContentTypeDefinition TestContentTypeDefinition;  
```  
  
 内容类型可以基于零个或多个预先存在的内容类型。 以下是内置类型：  
  
- 任何一个： 基本内容类型。 所有其他内容类型的父级。  
  
- 文本： 非投影内容基本类型。 从"任何"继承。  
  
- 纯文本： 对于非代码的文本。 继承自"text"。  
  
- 代码： 对于所有类型的代码。 继承自"text"。  
  
- 插入： 从任何类型的处理中排除的文本。 此内容类型的文本不会对其应用任何扩展。  
  
- 投影： 为投影缓冲区的内容。 从"任何"继承。  
  
- Intellisense： 为 IntelliSense 的内容。 继承自"text"。  
  
- Sighelp： 签名帮助。 从"intellisense"继承。  
  
- Sighelp doc： 签名帮助文档。 从"intellisense"继承。  
  
  以下是一些由 Visual Studio 定义的内容类型和一些 Visual Studio 中托管的语言：  
  
- Basic  
  
- C/C++  
  
- ConsoleOutput  
  
- CSharp  
  
- CSS  
  
- ENC  
  
- FindResults  
  
- F#  
  
- HTML  
  
- JScript  
  
- XAML  
  
- XML  
  
  若要发现可用的内容类型的列表，请导入<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>，可以维护在编辑器的内容类型的集合。 下面的代码将此服务作为属性导入。  
  
```  
[Import]  
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }  
```  
  
 若要将内容类型与文件扩展名相关联，请使用<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>。  
  
> [!NOTE]
> 在 Visual Studio 中，文件扩展名注册使用<xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute>的语言服务包。 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>将 MEF 内容类型与已在这种方式中注册的文件扩展名相关联。  
  
 若要导出到内容类型定义的文件扩展名，必须包含以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>： 指定的文件扩展名。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： 指定的内容类型。  
  
  因为<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>类密封的可以将其导出不使用任何类型参数。  
  
  下面的示例演示导出特性上的内容类型定义的文件名称扩展。  
  
```  
[Export]  
[FileExtension(".test")]  
[ContentType("test")]  
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;  
```  
  
 <xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>管理文件扩展名和内容类型之间的关联。  
  
## <a name="extending-classification-types-and-classification-formats"></a>扩展分类类型和分类设置格式  
 分类类型可用于定义你想要提供 （例如，显示蓝色的"关键字"文本和"comment"文本颜色为绿色） 的不同处理文本的类型。 通过声明类型的变量来定义新的分类类型<xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition>并为其赋予唯一名称。  
  
 若要使用编辑器注册分类类型，请将其导出以及以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 分类类型的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>： 此分类类型继承的分类类型的名称。 所有分类类型均都继承自"text"，并且分类类型可能都继承自多个其他分类类型。  
  
  因为<xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition>类密封的可以将其导出不使用任何类型参数。  
  
  下面的示例演示的分类类型定义导出特性。  
  
```  
[Export]  
[Name("csharp.test")]  
[BaseDefinition("test")]  
internal static ClassificationTypeDefinition CSharpTestDefinition;  
```  
  
 <xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>能够使用标准的分类。 其中包括内置分类类型：  
  
- “文本”  
  
- "自然语言"（从"text"派生而来）  
  
- "正式语言"（从"text"派生而来）  
  
- "string"（从"文本"派生而来）  
  
- "character"（从"文本"派生而来）  
  
- "数字"（从"文本"派生而来）  
  
  一组不同的错误类型继承自<xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition>。 它们包括以下的错误类型：  
  
- "语法错误"  
  
- "编译器错误"  
  
- "其他错误"  
  
- "warning"  
  
  若要发现可用分类类型的列表，请导入<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>，可以维护编辑器分类类型的集合。 下面的代码将此服务作为属性导入。  
  
```  
[Import]  
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }  
```  
  
 为新的分类类型，可以定义分类格式定义。 从派生类<xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition>并将其导出类型<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>一起使用具有以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 的格式的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>： 格式的显示名称。  
  
- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>： 指定是否在显示的格式**字体和颜色**页**选项**对话框。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>： 格式的优先级。 有效值为从<xref:Microsoft.VisualStudio.Text.Classification.Priority>。  
  
- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>： 此格式映射到类型分类的名称。  
  
  下面的示例显示了根据分类格式定义导出特性。  
  
```  
[Export(typeof(EditorFormatDefinition))]  
[ClassificationType(ClassificationTypeNames = "test")]  
[Name("test")]  
[DisplayName("Test")]  
[UserVisible(true)]  
[Order(After = Priority.Default, Before = Priority.High)]  
internal sealed class TestFormat : ClassificationFormatDefinition  
```  
  
 若要发现可用的格式的列表，请导入<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>，可以维护的格式为编辑器中的集合。 下面的代码将此服务作为属性导入。  
  
```  
[Import]  
internal IEditorFormatMapService FormatMapService { get; set; }  
```  
  
## <a name="extending-margins-and-scrollbars"></a>扩展的边距和滚动条  
 边距和滚动条是除了本身的文本视图编辑器的主视图元素。 您可以提供任意数量的除了文本视图周围出现的标准边距的边距。  
  
 实现<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin>接口可定义一个边距。 此外必须实现<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider>接口，以创建边距。  
  
 若要注册使用编辑器边距提供程序，必须导出提供程序和以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 边距的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 边距显示，相对于其他边距的顺序。  
  
   以下是内置边距：  
  
  - "Wpf 水平滚动条"  
  
  - "Wpf 垂直滚动条"  
  
  - "Wpf 行号边距"  
  
    有顺序的属性的水平边距`After="Wpf Horizontal Scrollbar"`如下所示的内置边距和有顺序的属性的水平边距`Before ="Wpf Horizontal Scrollbar"`显示上方的内置边距。 右键有顺序的属性的垂直边距`After="Wpf Vertical Scrollbar"`显示滚动条的右侧。 留有顺序的属性的垂直边距`After="Wpf Line Number Margin"`显示左侧的行号边距 （如果可见）。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>： 边距 （左、 右、 顶部或底部） 的类型。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： 在边距的有效内容 （例如，"text"或"代码"） 的类型。  
  
  下面的示例演示导出特性上将出现在右侧的行号边距的边距的边距提供程序。  
  
```  
[Export(typeof(IWpfTextViewMarginProvider))]  
[Name("TestMargin")]  
[Order(Before = "Wpf Line Number Margin")]  
[MarginContainer(PredefinedMarginNames.Left)]  
[ContentType("text")]   
```  
  
## <a name="extending-tags"></a>扩展标记  
 标记是文本的一种方法将数据与不同类型相关联。 在许多情况下，关联的数据显示为视觉效果，但不是所有标记都具有可视化表示形式。 您可以定义自己的标记的类型通过实现<xref:Microsoft.VisualStudio.Text.Tagging.ITag>。 此外必须实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>为一组给定的文本的 span，提供标记和<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>提供标记器。 必须导出标记器提供程序和以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： 你的标记的有效内容 （例如，"text"或"代码"） 的类型。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>： 标记的类型。  
  
  下面的示例演示导出特性标记器提供程序上。  
  
```  
[Export(typeof(ITaggerProvider))]  
[ContentType("text")]  
[TagType(typeof(TestTag))]  
internal class TestTaggerProvider : ITaggerProvider  
```  
  
 以下类型是标记的内置的：  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>： 与关联<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>： 与错误类型相关联。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>： 使用修饰与相关联。  
  
  > [!NOTE]
  > 有关的示例<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>，请参阅中的 HighlightWordTag 定义[演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>： 与可展开或折叠大纲显示中的区域相关联。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>： 在文本视图中定义的修饰所占用的空间。 有关空间协商修饰的详细信息，请参阅以下部分。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>： 提供自动的间距和大小调整为修饰。  
  
  若要查找和使用标记进行缓冲区和视图，导入<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>或<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>，这为您提供<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>的请求的类型。 下面的代码将此服务作为属性导入。  
  
```  
[Import]  
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }  
```  
  
#### <a name="tags-and-markerformatdefinitions"></a>标记和 MarkerFormatDefinitions  
 您可以扩展<xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>类定义的标记的外观。 必须将导出你的类 (作为<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>) 具有以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 用于引用此格式的名称  
  
- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>： 这将导致要在 UI 中显示的格式  
  
  在构造函数中，您定义的显示名称和标记的外观。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A> 定义填充颜色和<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A>定义的边框颜色。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A>格式定义的可本地化的名称。  
  
  下面是格式定义的示例：  
  
```  
[Export(typeof(EditorFormatDefinition))]  
[Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]  
[UserVisible(true)]  
internal class HighlightWordFormatDefinition : MarkerFormatDefinition  
{  
    public HighlightWordFormatDefinition()  
    {  
        this.BackgroundColor = Colors.LightBlue;  
        this.ForegroundColor = Colors.DarkBlue;  
        this.DisplayName = "Highlight Word";   
        this.ZOrder = 5;  
    }  
}  
  
```  
  
 若要将此格式定义应用于一个标记，引用类 （而不是显示名称） 的名称属性中设置的名称。  
  
> [!NOTE]
> 有关的示例<xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>，请参阅中的 HighlightWordFormatDefinition 类[演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)。  
  
## <a name="extending-adornments"></a>扩展修饰  
 修饰定义可添加到文本视图中显示的文本或文本视图自身中的视觉效果。 可以为任何类型的定义您自己修饰<xref:System.Windows.UIElement>。  
  
 在修饰类中，您必须声明<xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition>。 若要注册您修饰的层，将其导出以及以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 修饰的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>： 相对于其他修饰层修饰的顺序。 类<xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers>定义默认的四个层：选择、 大纲显示、 插入符号和文本。  
  
  下面的示例演示在修饰层定义导出特性。  
  
```  
[Export]  
[Name("TestEmbeddedAdornment")]  
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
internal AdornmentLayerDefinition testLayerDefinition;  
```  
  
 必须创建另一个类实现<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>，并处理其<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>通过实例化修饰的事件。 必须导出此类以及以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： 为其修饰是有效的内容 （例如，"text"或"代码"） 类型。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>： 此修饰的有效文本视图的类型。 类<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles>具有的预定义的文本视图角色集。 例如，<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>主要用于文本视图的文件。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> 用于文本视图，用户可以编辑或使用鼠标和键盘导航。 示例<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>视图是编辑器文本视图和**输出**窗口。  
  
  下面的示例演示导出特性修饰提供程序上。  
  
```  
[Export(typeof(IWpfTextViewCreationListener))]  
[ContentType("csharp")]  
[TextViewRole(PredefinedTextViewRoles.Document)]  
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener  
```  
  
 空间协调修饰是指占据空间处于同一级别的文本。 若要创建这种类型的修饰，必须定义标记类，该类继承<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>，用于定义修饰占用的空间量。  
  
 与所有修饰，则必须导出修饰层定义。  
  
```  
[Export]  
[Name("TestAdornment")]  
[Order(After = DefaultAdornmentLayers.Text)]  
internal AdornmentLayerDefinition testAdornmentLayer;  
```  
  
 若要实例化空间协调修饰，必须创建实现的类<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>，实现的类除了<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>（如使用其他类型的修饰）。  
  
 若要注册的标记器提供程序，必须将其导出以及以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： 在修饰的有效内容 （例如，"text"或"代码"） 的类型。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>： 此文本视图的类型标记或修饰是否有效。 类<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles>具有的预定义的文本视图角色集。 例如，<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>主要用于文本视图的文件。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> 用于文本视图，用户可以编辑或使用鼠标和键盘导航。 示例<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>视图是编辑器文本视图和**输出**窗口。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>： 类型的标记或已定义的修饰。 必须将添加第二个<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>为<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>。  
  
  下面的示例演示导出特性上的空间协商修饰标记标记器提供程序。  
  
```  
[Export(typeof(ITaggerProvider))]  
[ContentType("text")]  
[TextViewRole(PredefinedTextViewRoles.Document)]  
[TagType(typeof(SpaceNegotiatingAdornmentTag))]  
[TagType(typeof(TestSpaceNegotiatingTag))]  
internal sealed class TestTaggerProvider : ITaggerProvider  
```  
  
## <a name="extending-mouse-processors"></a>扩展鼠标处理器  
 您可以添加的鼠标输入的特殊处理。 创建继承自一个类<xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase>并重写的输入你想要处理的鼠标事件。 此外必须实现<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider>中第二个类并将其连同导出<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>指定鼠标处理程序的有效内容 （例如，"text"或"代码"） 的类型。  
  
 下面的示例显示了鼠标处理器提供程序上的导出特性。  
  
```  
[Export(typeof(IMouseProcessorProvider))]  
[Name("test mouse processor")]  
[ContentType("text")]  
[TextViewRole(PredefinedTextViewRoles.Interactive)]   
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider  
```  
  
## <a name="extending-drop-handlers"></a>扩展拖放处理程序  
 可以通过创建实现的类来自定义特定类型的文本的拖放处理程序的行为<xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler>和第二个类，用以实现<xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider>创建拖放处理程序。 必须将导出的拖放处理程序以及以下属性：  
  
- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>： 此拖放处理程序的有效的文本格式。 按从最高到低的优先级顺序处理以下格式：  
  
  1. 任何自定义格式  
  
  2. FileDrop  
  
  3. EnhancedMetafile  
  
  4. WaveAudio  
  
  5. Riff  
  
  6. 差异  
  
  7. 区域设置  
  
  8. 调色板  
  
  9. PenData  
  
  10. 可序列化  
  
  11. SymbolicLink  
  
  12. Xaml  
  
  13. XamlPackage  
  
  14. Tiff  
  
  15. Bitmap  
  
  16. Dib  
  
  17. MetafilePicture  
  
  18. CSV  
  
  19. System.String  
  
  20. HTML 格式  
  
  21. UnicodeText  
  
  22. OEMText  
  
  23. Text  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 删除处理程序的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>： 之前或之后默认拖放处理程序拖放处理程序的顺序。 Visual Studio 默认拖放处理程序命名为"DefaultFileDropHandler"。  
  
  下面的示例演示导出特性上拖放处理程序提供程序。  
  
```  
[Export(typeof(IDropHandlerProvider))]  
[DropFormat("Text")]   
[Name("TestDropHandler")]  
[Order(Before="DefaultFileDropHandler")]   
internal class TestDropHandlerProvider : IDropHandlerProvider  
```  
  
## <a name="extending-editor-options"></a>扩展编辑器选项  
 您可以定义为仅在特定范围，例如，在文本视图中有效的选项。 编辑器提供了此组的预定义的选项： 编辑器选项、 视图选项和 Windows Presentation Foundation (WPF) 视图选项。 这些选项可在<xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions>， <xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions>，和<xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions>。  
  
 若要添加一个新的选项，请从这些选项定义类之一派生一个类：  
  
- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>  
  
- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>  
  
- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>  
  
  下面的示例显示了如何导出选项定义具有一个布尔值。  
  
```  
[Export(typeof(EditorOptionDefinition))]  
internal sealed class TestOption : EditorOptionDefinition<bool>  
```  
  
## <a name="extending-intellisense"></a>扩展 IntelliSense  
 IntelliSense 是一组提供有关结构化文本的信息的功能的常规术语和它的语句完成。 这些功能包括语句完成、 签名帮助、 快速信息和灯泡。 语句完成有助于正确键入的语言关键字或成员名称的用户。 签名帮助显示签名或签名的用户只需具有类型化的方法。 当鼠标停留在其上时，快速信息将显示类型或成员名称的完整签名。 灯泡提供在重命名一个匹配项之后重命名变量的所有匹配项的某些上下文中，例如，在某些标识符的其他操作。  
  
 IntelliSense 功能的设计是在所有情况下非常相似：  
  
- IntelliSense *broker*负责整个过程。  
  
- IntelliSense*会话*表示之间的表示器并或取消所选内容的触发事件的顺序。 某些用户手势通常触发该会话。  
  
- IntelliSense*控制器*负责决定会话应开始和结束时。 它还会决定信息应提交和时，应取消会话。  
  
- IntelliSense*源*提供内容，并决定最佳匹配项。  
  
- IntelliSense *presenter*负责显示内容。  
  
  在大多数情况下，我们建议你提供的控制器和至少一个源。 如果你想要自定义显示内容，还可以提供表示器。  
  
### <a name="implementing-an-intellisense-source"></a>实现智能感知源  
 若要自定义源，必须实现一个 （或多个） 的以下源接口：  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>  
  
> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource> 已弃用的<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>。  
  
 此外，必须实现相同类型的提供的程序：  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>  
  
> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider> 已弃用的<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>。  
  
 必须导出提供程序和以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 源的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： 源适用的内容 （例如，"text"或"代码"） 类型。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>： 源应 （相对于其他源） 的显示的顺序。  
  
- 下面的示例显示了完成源提供程序上的导出特性。  
  
```  
Export(typeof(ICompletionSourceProvider))]  
[Name(" Test Statement Completion Provider")]  
[Order(Before = "default")]  
[ContentType("text")]  
internal class TestCompletionSourceProvider : ICompletionSourceProvider  
```  
  
 有关实现 IntelliSense 源的详细信息，请参阅以下演练：  
  
 [演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)  
  
 [演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)  
  
 [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)  
  
### <a name="implementing-an-intellisense-controller"></a>实现智能感知控制器  
 若要自定义控制器，则必须实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>接口。 此外，必须实现控制器提供程序以及以下属性：  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>： 控制器的名称。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： 在控制器适用的内容 （例如，"text"或"代码"） 类型。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>： 在控制器应 （相对于其他控制器） 的显示的顺序。  
  
  下面的示例显示了完成控制器提供程序上的导出特性。  
  
```  
Export(typeof(IIntellisenseControllerProvider))]  
[Name(" Test Controller Provider")]  
[Order(Before = "default")]  
[ContentType("text")]  
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider  
```  
  
 有关使用 IntelliSense 控制器的详细信息，请参阅以下演练：  
  
 [演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)
