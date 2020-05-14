---
title: 语言服务和编辑器扩展点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extension points
ms.assetid: 91a6417e-a6fe-4bc2-9d9f-5173c634a99b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 28bb086eb99e4b8128c04f62f9b370eb2eab8fa3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703048"
---
# <a name="language-service-and-editor-extension-points"></a>语言服务和编辑器扩展点
编辑器提供扩展点，您可以将扩展为托管扩展框架 （MEF） 组件，包括大多数语言服务功能。 这些是主要扩展点类别：

- 内容类型

- 分类类型和分类格式

- 边距和滚动条

- Tags

- 装饰品

- 鼠标处理器

- 放置处理程序

- 选项

- IntelliSense

## <a name="extend-content-types"></a>扩展内容类型
 内容类型是编辑器处理的文本类型的定义，例如"文本"、"代码"或"CSharp"。 通过声明类型的<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>变量并给新内容类型指定唯一名称，可以定义新的内容类型。 要向编辑器注册内容类型，请将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>是内容类型的名称。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>是派生此内容类型的内容类型的名称。 内容类型可能从多个其他内容类型继承。

  由于类<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>是密封的，因此无需类型参数即可导出它。

  下面的示例显示内容类型定义上的导出属性。

```
[Export]
[Name("test")]
[BaseDefinition("code")]
[BaseDefinition("projection")]
internal static ContentTypeDefinition TestContentTypeDefinition;
```

 内容类型可以基于零个或多个预先存在的内容类型。 这些是内置类型：

- 任何：基本内容类型。 所有其他内容类型的父级。

- 文本：非投影内容的基本类型。 从"任意"继承。

- 纯文本：用于非代码文本。 从"文本"继承。

- 代码：用于各种代码。 从"文本"继承。

- 惰性：从任何类型的处理中排除文本。 此内容类型的文本永远不会应用任何扩展。

- 投影：用于投影缓冲区的内容。 从"任意"继承。

- 感知：对于IntelliSense的内容。 从"文本"继承。

- Sighelp：签名帮助。 从"理智"继承。

- Sighelp-doc：签名帮助文档。 从"理智"继承。

  以下是由 Visual Studio 定义的一些内容类型，以及 Visual Studio 中托管的一些语言：

- Basic

- C/C++

- 控制台输出

- CSharp

- CSS

- ENC

- 查找结果

- F#

- HTML

- JScript

- XAML

- XML

  要发现可用内容类型的列表，导入 ，<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>该列表维护编辑器的内容类型的集合。 以下代码将此服务导入为属性。

```
[Import]
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }
```

 要将内容类型与文件名扩展名相关联，请使用<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>。

> [!NOTE]
> 在 Visual Studio 中，使用<xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute>语言服务包注册文件名扩展名。 将<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>MEF 内容类型与以这种方式注册的文件名扩展名关联。

 要将文件名扩展名导出到内容类型定义，必须包括以下属性：

- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>：指定文件名扩展名。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：指定内容类型。

  由于类<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>是密封的，因此无需类型参数即可导出它。

  下面的示例显示内容类型定义的文件名扩展名上的导出属性。

```
[Export]
[FileExtension(".test")]
[ContentType("test")]
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;
```

 管理<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>文件名扩展名和内容类型之间的关联。

## <a name="extend-classification-types-and-classification-formats"></a>扩展分类类型和分类格式
 可以使用分类类型来定义要为其提供不同处理的文本类型（例如，将"关键字"文本着色为蓝色和"注释"文本为绿色）。 通过声明类型的<xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition>变量并给它指定唯一名称来定义新的分类类型。

 要向编辑器注册分类类型，请将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：分类类型的名称。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>：此分类类型继承的分类类型的名称。 所有分类类型都从"文本"继承，分类类型可能从多个其他分类类型继承。

  由于类<xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition>是密封的，因此无需类型参数即可导出它。

  下面的示例在分类类型定义上显示导出属性。

```
[Export]
[Name("csharp.test")]
[BaseDefinition("test")]
internal static ClassificationTypeDefinition CSharpTestDefinition;
```

 提供<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>对标准分类的访问。 内置分类类型包括：

- "text"

- "自然语言"（源自"文本"）

- "正式语言"（源自"文本"）

- "字符串"（派生自"文本"）

- "字符"（派生自"文字"）

- "数字"（派生自"文字"）

  从 继承的<xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition>一组不同的错误类型。 它们包括以下错误类型：

- "语法错误"

- "编译器错误"

- "其他错误"

- "警告"

  要发现可用分类类型的列表，导入 ，<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>该列表维护编辑器的分类类型的集合。 以下代码将此服务导入为属性。

```
[Import]
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }
```

 您可以为新分类类型定义分类格式定义。 从<xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition>派生类，并导出它与类型<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>，以及以下属性：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：格式的名称。

- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>：格式的显示名称。

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>：指定格式是否显示在 **"选项**"对话框的"**字体和颜色**"页上。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：格式的优先级。 有效值来自<xref:Microsoft.VisualStudio.Text.Classification.Priority>。

- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>：映射此格式的分类类型的名称。

  下面的示例在分类格式定义上显示导出属性。

```
[Export(typeof(EditorFormatDefinition))]
[ClassificationType(ClassificationTypeNames = "test")]
[Name("test")]
[DisplayName("Test")]
[UserVisible(true)]
[Order(After = Priority.Default, Before = Priority.High)]
internal sealed class TestFormat : ClassificationFormatDefinition
```

 要发现可用格式的列表，导入 ，<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>该列表维护编辑器的格式集合。 以下代码将此服务导入为属性。

```
[Import]
internal IEditorFormatMapService FormatMapService { get; set; }
```

## <a name="extend-margins-and-scrollbars"></a>扩展边距和滚动条
 边距和滚动条是编辑器的主要视图元素，除了文本视图本身。 除了文本视图周围显示的标准边距之外，还可以提供任意数量的边距。

 实现接口<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin>以定义边距。 还必须实现<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider>接口以创建边距。

 要向编辑器注册边距提供程序，必须导出提供程序以及以下属性：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：边距的名称。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：相对于其他边距，边距的显示顺序。

   这些是内置边距：

  - "Wpf 水平滚动条"

  - "Wpf 垂直滚动条"

  - "Wpf 行号边距"

    具有 order`After="Wpf Horizontal Scrollbar"`属性的水平边距显示在内置边距下方，具有 订单`Before ="Wpf Horizontal Scrollbar"`属性的水平边距显示在内置边距上方。 具有 顺序`After="Wpf Vertical Scrollbar"`属性的右垂直边距显示在滚动条的右侧。 具有 order 属性的`After="Wpf Line Number Margin"`左侧垂直边距显示在行号边距的左侧（如果可见）。

- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>：边距类型（左、右、上或下）。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：您的边距有效的内容类型（例如，"文本"或"代码"）。

  下面的示例显示行号边距右侧的边距提供商上的导出属性。

```
[Export(typeof(IWpfTextViewMarginProvider))]
[Name("TestMargin")]
[Order(Before = "Wpf Line Number Margin")]
[MarginContainer(PredefinedMarginNames.Left)]
[ContentType("text")]
```

## <a name="extend-tags"></a>扩展标记
 标记是将数据与不同类型的文本关联的一种方式。 在许多情况下，关联的数据显示为视觉效果，但并非所有标记都有可视表示。 您可以通过实现<xref:Microsoft.VisualStudio.Text.Tagging.ITag>来定义自己的标记类型。 还必须实现<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>为给定的文本范围集提供标记，并为<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>提供标记器。 您必须导出标记提供程序以及以下属性：

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：标记有效的内容类型（例如，"文本"或"代码"）。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>：标记的种类。

  下面的示例显示标记提供程序上的导出属性。

\<代码内容霍尔德>8</CodeContentPlaceHolder>以下类型的标记是内置的：

- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>： 与<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>关联。

- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>：与错误类型关联。

- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>：与修饰相关联。

  > [!NOTE]
  > 有关 的示例<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>，请参阅演练中的高光字标签定义[：突出显示文本](../extensibility/walkthrough-highlighting-text.md)。

- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>：与可在大纲中展开或折叠的区域关联。

- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>：定义修饰在文本视图中占用的空间。 有关空间协商装饰的详细信息，请参阅以下部分。

- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>：为装饰提供自动间距和大小调整。

  要查找和使用缓冲区和视图的标记，请导入 提供<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>请求类型的<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>的 或<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>。 以下代码将此服务导入为属性。

```
[Import]
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }
```

#### <a name="tags-and-markerformatdefinitions"></a>标记和标记格式定义
 可以扩展类<xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>以定义标记的外观。 您必须使用以下属性导出类 （<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>作为 ）：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：用于引用此格式的名称

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>：这将导致格式显示在 UI 中

  在构造函数中，定义标记的显示名称和外观。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A>定义填充颜色，并<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A>定义边框颜色。 是<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A>格式定义的可本地化名称。

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

 要将此格式定义应用于标记，请引用在类的名称属性（而不是显示名称）中设置的名称。

> [!NOTE]
> 有关 的示例<xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>，请参阅演练中的高光字格式定义类[：突出显示文本](../extensibility/walkthrough-highlighting-text.md)。

## <a name="extend-adornments"></a>扩展装饰
 装饰定义可以添加到文本视图中显示的文本或文本视图本身的视觉效果。 您可以将自己的修饰定义为任何类型的<xref:System.Windows.UIElement>。

 在修饰类中，必须声明 。 <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> 要注册修饰图层，请将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：修饰的名称。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：相对于其他装饰层的修饰顺序。 该类<xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers>定义四个默认图层：选择、大纲、Caret 和文本。

  下面的示例显示修饰图层定义上的导出属性。

```
[Export]
[Name("TestEmbeddedAdornment")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
internal AdornmentLayerDefinition testLayerDefinition;
```

 您必须创建第二个类，通过<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>实例化修饰<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>实现和处理其事件。 您必须将此类与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：修饰有效的内容类型（例如，"文本"或"代码"）。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>：此修饰有效的文本视图类型。 类<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles>具有预定义的文本视图角色集。 例如，<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>主要用于文件的文本视图。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>用于用户可以使用鼠标和键盘编辑或导航的文本视图。 视图的示例<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>包括编辑器文本视图和 **"输出"** 窗口。

  下面的示例显示修饰提供程序上的导出属性。

```
[Export(typeof(IWpfTextViewCreationListener))]
[ContentType("csharp")]
[TextViewRole(PredefinedTextViewRoles.Document)]
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener
```

 空间协商修饰是指占用与文本相同的空间的修饰。 要创建此类修饰，必须定义从<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>继承的标记类，该类定义修饰占用的空间量。

 与所有修饰一样，必须导出修饰图层定义。

```
[Export]
[Name("TestAdornment")]
[Order(After = DefaultAdornmentLayers.Text)]
internal AdornmentLayerDefinition testAdornmentLayer;
```

 要实例化空间协商修饰，除了实现<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider><xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>的类（与其他类型的修饰一样），还必须创建实现的类。

 要注册标记提供程序，必须将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：装饰有效的内容类型（例如，"文本"或"代码"）。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>：此标记或修饰有效的文本视图类型。 类<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles>具有预定义的文本视图角色集。 例如，<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>主要用于文件的文本视图。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>用于用户可以使用鼠标和键盘编辑或导航的文本视图。 视图的示例<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>包括编辑器文本视图和 **"输出"** 窗口。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>：您定义的标记或修饰类型。 必须为<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>添加第<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>二秒。

  下面的示例显示标记器提供程序上的空间协商修饰标记的导出属性。

```
[Export(typeof(ITaggerProvider))]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Document)]
[TagType(typeof(SpaceNegotiatingAdornmentTag))]
[TagType(typeof(TestSpaceNegotiatingTag))]
internal sealed class TestTaggerProvider : ITaggerProvider
```

## <a name="extending-mouse-processors"></a>扩展鼠标处理器
 您可以为鼠标输入添加特殊处理。 创建从继承<xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase>和覆盖要处理的输入的鼠标事件的类。 还必须在第二个<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider>类中实现，并将其与<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>指定鼠标处理程序有效的内容类型（例如，"文本"或"代码"）一起导出。

 下面的示例显示鼠标处理器提供程序上的导出属性。

```
[Export(typeof(IMouseProcessorProvider))]
[Name("test mouse processor")]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Interactive)]
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider
```

## <a name="extend-drop-handlers"></a>扩展放置处理程序
 可以通过创建实现<xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler>的类和第二个实现<xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider>以创建放置处理程序的类来自定义特定文本类型的放置处理程序的行为。 您必须导出放置处理程序以及以下属性：

- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>：此放置处理程序有效的文本格式。 以下格式按优先级顺序从最高到最低的顺序处理：

  1. 任何自定义格式

  2. 文件丢弃

  3. 增强元文件

  4. 波迪奥

  5. 里夫

  6. 迪夫

  7. Locale

  8. 调色板

  9. 笔数据

  10. 可序列化

  11. 符号链接

  12. Xaml

  13. Xaml 包装

  14. Tiff

  15. Bitmap

  16. 迪布

  17. 元文件图片

  18. CSV

  19. System.String

  20. HTML 格式

  21. Unicode文本

  22. OEM文本

  23. Text

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：放置处理程序的名称。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：在默认放置处理程序之前或之后放置处理程序的顺序。 Visual Studio 的默认放置处理程序名为"默认文件删除处理程序"。

  下面的示例显示放置处理程序提供程序上的导出属性。

```
[Export(typeof(IDropHandlerProvider))]
[DropFormat("Text")]
[Name("TestDropHandler")]
[Order(Before="DefaultFileDropHandler")]
internal class TestDropHandlerProvider : IDropHandlerProvider
```

## <a name="extending-editor-options"></a>扩展编辑器选项
 可以将选项定义为仅在特定作用域中有效，例如，在文本视图中。 编辑器提供这组预定义选项：编辑器选项、视图选项和 Windows 演示文稿基础 （WPF） 视图选项。 可以在<xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions>中找到这些选项 ，<xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions>和<xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions>。

 要添加新选项，可以从以下选项定义类之一派生类：

- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>

  下面的示例演示如何导出具有布尔值的选项定义。

```
[Export(typeof(EditorOptionDefinition))]
internal sealed class TestOption : EditorOptionDefinition<bool>
```

## <a name="extend-intellisense"></a>扩展感知
 IntelliSense 是一组功能的通用术语，提供有关结构化文本的信息并为其完成语句。 这些功能包括语句完成、签名帮助、快速信息和灯泡。 语句完成可帮助用户正确键入语言关键字或成员名称。 签名帮助显示用户刚刚键入的方法的签名或签名。 当鼠标停留在该类型或成员名称上时，快速信息将显示类型或成员名称的完整签名。 灯泡为某些上下文中的某些标识符提供其他操作，例如，重命名变量的所有匹配项后重命名一个发生情况。

 在所有情况下，IntelliSense 功能的设计都大致相同：

- IntelliSense*经纪商*负责整个流程。

- IntelliSense*会话*表示演示者触发与提交或取消所选内容之间的事件序列。 会话通常由某些用户手势触发。

- IntelliSense*控制器*负责决定会话何时开始和结束。 它还决定何时提交信息以及何时取消会话。

- IntelliSense*源*提供内容并决定最佳匹配项。

- IntelliSense*演示者*负责显示内容。

  在大多数情况下，我们建议您至少提供源和控制器。 如果要自定义显示，还可以提供演示者。

### <a name="implement-an-intellisense-source"></a>实现感知源
 要自定义源，必须实现以下源接口的一个或多个：

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource>已被弃用，<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>以赞成 。

 此外，您必须实现同一类型的提供程序：

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider>已被弃用，<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>以赞成 。

 您必须将提供程序与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：源的名称。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：源应用于的内容类型（例如，"文本"或"代码"）。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：源应显示的顺序（相对于其他源）。

- 下面的示例显示完成源提供程序上的导出属性。

```
Export(typeof(ICompletionSourceProvider))]
[Name(" Test Statement Completion Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestCompletionSourceProvider : ICompletionSourceProvider
```

 有关实现 IntelliSense 源的详细信息，请参阅以下演练：

- [演练：显示快速信息工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)

- [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)

### <a name="implement-an-intellisense-controller"></a>实现 IntelliSense 控制器
 要自定义控制器，必须实现<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>接口。 此外，必须实现控制器提供程序以及以下属性：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：控制器的名称。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：控制器应用的内容类型（例如，"文本"或"代码"）。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：控制器的显示顺序（相对于其他控制器）。

  下面的示例显示完成控制器提供程序上的导出属性。

```
Export(typeof(IIntellisenseControllerProvider))]
[Name(" Test Controller Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider
```

 有关使用 IntelliSense 控制器的详细信息，请参阅以下演练：

- [演练：显示快速信息工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)
