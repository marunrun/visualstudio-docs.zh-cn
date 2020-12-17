---
title: 语言服务和编辑器扩展点 |Microsoft Docs
description: 了解可扩展的 Visual Studio 代码编辑器中的扩展点，包括大多数语言服务功能。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 06329fcfcefe3ea75b772495f6a7e0dd14ced087
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97615546"
---
# <a name="language-service-and-editor-extension-points"></a>语言服务和编辑器扩展点
编辑器提供了扩展点，您可以将其作为 Managed Extensibility Framework (MEF) 组件部件（包括大多数语言服务功能）扩展。 下面是主要扩展点类别：

- 内容类型

- 分类类型和分类格式

- 边距和滚动条

- 标记

- 修饰

- 鼠标处理器

- 删除处理程序

- 选项

- IntelliSense

## <a name="extend-content-types"></a>扩展内容类型
 内容类型是由编辑器处理的文本种类的定义，例如 "text"、"code" 或 "CSharp"。 通过声明类型的变量 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> 并为新内容类型提供唯一名称，可以定义新的内容类型。 若要在编辑器中注册内容类型，请将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 内容类型的名称。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute> 此内容类型派生自的内容类型的名称。 内容类型可以从其他多个内容类型继承。

  由于 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> 该类是密封的，因此可以在不包含任何类型参数的情况下将其导出。

  下面的示例演示如何导出内容类型定义的属性。

```
[Export]
[Name("test")]
[BaseDefinition("code")]
[BaseDefinition("projection")]
internal static ContentTypeDefinition TestContentTypeDefinition;
```

 内容类型可以基于零个或多个预先存在的内容类型。 这些是内置类型：

- Any：基本内容类型。 所有其他内容类型的父。

- Text：非投影内容的基本类型。 继承自 "any"。

- 纯文本：对于非代码文本。 继承自 "text"。

- 代码：用于所有类型的代码。 继承自 "text"。

- 静态：排除任何类型的处理中的文本。 此内容类型的文本将永远不会应用任何扩展。

- 投影：用于投影缓冲区的内容。 继承自 "any"。

- Intellisense：对于 IntelliSense 的内容。 继承自 "text"。

- Sighelp：签名帮助。 继承自 "intellisense"。

- Sighelp：签名帮助文档。 继承自 "intellisense"。

  下面是 Visual Studio 定义的一些内容类型，以及 Visual Studio 中承载的一些语言：

- 基本

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

  若要发现可用内容类型的列表，请导入 <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> ，后者维护编辑器的内容类型集合。 下面的代码将此服务作为属性导入。

```
[Import]
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }
```

 若要将内容类型与文件扩展名关联，请使用 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> 。

> [!NOTE]
> 在 Visual Studio 中，文件扩展名是通过 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute> 对语言服务包使用来注册的。 将 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> MEF 内容类型与已以这种方式注册的文件扩展名相关联。

 若要将文件扩展名导出到内容类型定义中，必须包括以下属性：

- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>：指定文件扩展名。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：指定内容类型。

  由于 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> 该类是密封的，因此可以在不包含任何类型参数的情况下将其导出。

  下面的示例演示如何将文件扩展名的属性导出到内容类型定义。

```
[Export]
[FileExtension(".test")]
[ContentType("test")]
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;
```

 <xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>管理文件扩展名和内容类型之间的关联。

## <a name="extend-classification-types-and-classification-formats"></a>扩展分类类型和分类格式
 您可以使用分类类型来定义要为其提供不同处理 (的文本类型，例如，将 "关键字" 文本蓝色和 "注释" 文本着色) 。 通过声明类型的变量 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> 并为其提供唯一名称来定义新的分类类型。

 若要向编辑器注册分类类型，请将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：分类类型的名称。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>：此分类类型继承的分类类型的名称。 所有分类类型都继承自 "text"，分类类型可继承自其他多个分类类型。

  由于 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> 该类是密封的，因此可以在不包含任何类型参数的情况下将其导出。

  下面的示例显示了如何导出分类类型定义的属性。

```
[Export]
[Name("csharp.test")]
[BaseDefinition("test")]
internal static ClassificationTypeDefinition CSharpTestDefinition;
```

 <xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>提供对标准分类的访问。 内置分类类型包括：

- "text"

- "自然语言" (派生自 "text" ) 

- "正式语言" (派生自 "text" ) 

- "string" (派生自 "literal" ) 

- "字符" (派生自 "literal" ) 

- "数字" (派生自 "literal" ) 

  从继承的一组不同的错误类型 <xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition> 。 它们包括以下错误类型：

- "语法错误"

- "编译器错误"

- "其他错误"

- 出现

  若要发现可用分类类型的列表，请导入 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> ，后者维护编辑器的分类类型集合。 下面的代码将此服务作为属性导入。

```
[Import]
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }
```

 你可以为新的分类类型定义分类格式定义。 从派生类 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition> 并将其与类型一起导出 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> ，并与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：格式的名称。

- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>：格式的显示名称。

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>：指定格式是否出现在 "**选项**" 对话框的 "**字体和颜色**" 页上。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：格式的优先级。 有效的值来自 <xref:Microsoft.VisualStudio.Text.Classification.Priority> 。

- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>：此格式所映射到的分类类型的名称。

  下面的示例演示如何在分类格式定义上导出属性。

```
[Export(typeof(EditorFormatDefinition))]
[ClassificationType(ClassificationTypeNames = "test")]
[Name("test")]
[DisplayName("Test")]
[UserVisible(true)]
[Order(After = Priority.Default, Before = Priority.High)]
internal sealed class TestFormat : ClassificationFormatDefinition
```

 若要发现可用格式的列表，请导入 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> ，其中维护编辑器的格式集合。 下面的代码将此服务作为属性导入。

```
[Import]
internal IEditorFormatMapService FormatMapService { get; set; }
```

## <a name="extend-margins-and-scrollbars"></a>扩展边距和滚动条
 除了文本视图本身，边距和滚动条是编辑器的主要视图元素。 除了文本视图周围显示的标准边距，还可以提供任意数量的边距。

 实现 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin> 接口以定义边距。 还必须实现 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> 接口才能创建边距。

 若要将边距提供程序注册到编辑器，你必须将该提供程序与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：边距的名称。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：边距相对于其他边距的显示顺序。

   以下为内置边距：

  - "Wpf 水平滚动条"

  - "Wpf 垂直滚动条"

  - "Wpf 行号边距"

    顺序属性为的水平边距显示在 `After="Wpf Horizontal Scrollbar"` 内置边距下，并且具有顺序属性的水平边距 `Before ="Wpf Horizontal Scrollbar"` 显示在内置边距上方。 顺序属性为的右垂直边距 `After="Wpf Vertical Scrollbar"` 将显示在滚动条的右侧。 排序属性为的左垂直边距显示在 `After="Wpf Line Number Margin"` 行号边距左侧 (如果它在) 可见。

- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>：页边距 (左、右、上或下) 。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：内容的类型 (例如，边距有效的 "text" 或 "code" ) 。

  下面的示例演示如何导出边距提供程序的属性，以获取显示在行号边距右侧的边距。

```
[Export(typeof(IWpfTextViewMarginProvider))]
[Name("TestMargin")]
[Order(Before = "Wpf Line Number Margin")]
[MarginContainer(PredefinedMarginNames.Left)]
[ContentType("text")]
```

## <a name="extend-tags"></a>扩展标记
 标记是将数据与不同类型的文本相关联的一种方法。 在许多情况下，关联的数据显示为视觉效果，但并不是所有标记都具有视觉对象。 可以通过实现来定义自己的标记类型 <xref:Microsoft.VisualStudio.Text.Tagging.ITag> 。 您还必须实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 以便为一组给定的文本跨度提供标记，并使用 <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> 来提供标记。 必须将标记提供程序与下列属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>： (的内容类型（例如，"text" 或 "code" ) ，你的标记是有效的）。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>：标记的类型。

  下面的示例演示如何在标记提供程序上导出特性。

\<CodeContentPlaceHolder>8 </CodeContentPlaceHolder> 以下类型的标记是内置的：

- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>：与关联 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> 。

- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>：与错误类型相关联。

- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>：与修饰关联。

  > [!NOTE]
  > 有关的示例 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ，请参阅 [演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)中的 HighlightWordTag 定义。

- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>：与可在大纲显示中展开或折叠的区域关联。

- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>：定义修饰在文本视图中所占据的空间。 有关空间协调修饰的详细信息，请参阅下一节。

- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>：提供修饰的自动间距和大小调整。

  若要查找缓冲区和视图的标记并使用这些标记，请导入 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService> 或 <xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService> ，这将为你提供所 <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> 请求的类型。 下面的代码将此服务作为属性导入。

```
[Import]
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }
```

#### <a name="tags-and-markerformatdefinitions"></a>标记和 MarkerFormatDefinitions
 您可以扩展 <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> 类以定义标记的外观。 您必须将您的类 (作为 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> 具有以下特性的) 导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：用于引用此格式的名称

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>：这将导致在 UI 中显示格式

  在构造函数中，定义标记的显示名称和外观。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A> 定义填充颜色，并 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A> 定义边框颜色。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A>是格式定义的可本地化的名称。

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

 若要将此格式定义应用于标记，请引用在类的 "名称" 属性中设置的名称， (不是显示名称) 。

> [!NOTE]
> 有关的示例 <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> ，请参阅 [演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)中的 HighlightWordFormatDefinition 类。

## <a name="extend-adornments"></a>扩展修饰
 修饰可定义视觉效果，这些效果可以添加到文本视图中显示的文本或文本视图本身。 您可以将自己的修饰定义为任意类型的 <xref:System.Windows.UIElement> 。

 在修饰类中，必须声明 <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> 。 若要注册修饰层，请将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：修饰的名称。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：与其他修饰层相关的修饰的排序。 类 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers> 定义四个默认层：选择、大纲显示、插入符号和文本。

  下面的示例演示如何在修饰层定义上导出特性。

```
[Export]
[Name("TestEmbeddedAdornment")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
internal AdornmentLayerDefinition testLayerDefinition;
```

 您必须创建另一个实现 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> 并 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 通过实例化修饰来处理其事件的类。 必须将此类与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：内容的类型 (例如，修饰对其有效的 "text" 或 "code" ) 。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>：此修饰有效的文本视图的类型。 类 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> 具有一组预定义的文本视图角色。 例如， <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> 主要用于文件的文本视图。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> 用于用户可以使用鼠标和键盘编辑或导航的文本视图。 视图的示例 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> 包括编辑器文本视图和 " **输出** " 窗口。

  下面的示例演示了如何在修饰提供程序上导出特性。

```
[Export(typeof(IWpfTextViewCreationListener))]
[ContentType("csharp")]
[TextViewRole(PredefinedTextViewRoles.Document)]
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener
```

 空间协商修饰是占用与文本处于相同级别的空间的修饰。 若要创建此类修饰，你必须定义一个继承自的标记类 <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> ，后者定义修饰所占用的空间量。

 与所有修饰一样，必须导出修饰层定义。

```
[Export]
[Name("TestAdornment")]
[Order(After = DefaultAdornmentLayers.Text)]
internal AdornmentLayerDefinition testAdornmentLayer;
```

 若要实例化空间协商修饰，您必须创建一个实现的类 <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> ，该类除了实现 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> 其他类型的修饰) 之外还实现 (。

 若要注册标记器提供程序，必须将其与以下属性一起导出：

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：内容的类型 (例如，修饰有效的 "text" 或 "code" ) 。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>：此标记或修饰有效的文本视图的类型。 类 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> 具有一组预定义的文本视图角色。 例如， <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> 主要用于文件的文本视图。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> 用于用户可以使用鼠标和键盘编辑或导航的文本视图。 视图的示例 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> 包括编辑器文本视图和 " **输出** " 窗口。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>：你定义的标记或修饰的类型。 您必须为添加另 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> 一个 <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> 。

  下面的示例演示如何在标记提供程序上为空格协调修饰标记导出特性。

```
[Export(typeof(ITaggerProvider))]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Document)]
[TagType(typeof(SpaceNegotiatingAdornmentTag))]
[TagType(typeof(TestSpaceNegotiatingTag))]
internal sealed class TestTaggerProvider : ITaggerProvider
```

## <a name="extending-mouse-processors"></a>扩展鼠标处理器
 您可以为鼠标输入添加特殊处理。 创建一个继承自的类 <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> ，并覆盖您要处理的输入的鼠标事件。 还必须 <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> 在另一个类中实现，并将其与 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 指定内容种类 (例如，"text" 或 "code" ) （您的鼠标处理程序有效）一起导出。

 下面的示例演示如何在鼠标处理器提供程序上导出属性。

```
[Export(typeof(IMouseProcessorProvider))]
[Name("test mouse processor")]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Interactive)]
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider
```

## <a name="extend-drop-handlers"></a>扩展删除处理程序
 您可以通过创建一个实现的类 <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler> ，并使用实现的另一个类 <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider> 来创建删除处理程序，从而为特定类型的文本自定义 drop 处理程序的行为。 您必须将 drop 处理程序与下列属性一起导出：

- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>：此放置处理程序有效的文本格式。 以下格式按优先级从高到低的顺序进行处理：

  1. 任何自定义格式

  2. FileDrop

  3. EnhancedMetafile

  4. WaveAudio

  5. Riff

  6. Dif

  7. Locale

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

  23. 文本

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：放置处理程序的名称。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：放置处理程序在默认放置处理程序之前或之后的顺序。 Visual Studio 的默认丢弃处理程序名为 "DefaultFileDropHandler"。

  下面的示例演示了如何在 drop handler 提供程序上导出属性。

```
[Export(typeof(IDropHandlerProvider))]
[DropFormat("Text")]
[Name("TestDropHandler")]
[Order(Before="DefaultFileDropHandler")]
internal class TestDropHandlerProvider : IDropHandlerProvider
```

## <a name="extending-editor-options"></a>扩展编辑器选项
 您可以定义仅在特定作用域（例如，在文本视图中）有效的选项。 编辑器提供此预定义选项集：编辑器选项、视图选项和 Windows Presentation Foundation (WPF) 视图选项。 可以在、和中找到这些选项 <xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions> <xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions> <xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions> 。

 若要添加新选项，请从以下选项定义类之一派生类：

- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>

  下面的示例演示如何导出具有布尔值的选项定义。

```
[Export(typeof(EditorOptionDefinition))]
internal sealed class TestOption : EditorOptionDefinition<bool>
```

## <a name="extend-intellisense"></a>扩展 IntelliSense
 IntelliSense 是一组功能的通用术语，提供有关结构化文本和语句完成的信息。 这些功能包括语句完成、签名帮助、快速信息和轻型电灯泡。 语句完成有助于用户正确地键入语言关键字或成员名称。 签名帮助显示用户刚刚键入的方法的签名或签名。 当鼠标停留在某个类型或成员名称上时，"快速信息" 显示该类型或成员名称的完整签名。 灯泡为某些上下文中的某些标识符提供其他操作，例如，重命名一个出现的变量后，重命名该变量的所有匹配项。

 在所有情况下，IntelliSense 功能的设计都是相同的：

- IntelliSense *broker* 负责整个过程。

- IntelliSense *会话* 表示在触发表示器与所选内容的提交或取消之间发生的事件的顺序。 会话通常由某些用户手势触发。

- IntelliSense *控制器* 负责确定会话应何时开始和结束。 它还决定何时应提交信息以及何时应取消会话。

- IntelliSense *源* 提供内容并确定最佳匹配项。

- *IntelliSense 显示器负责显示* 内容。

  在大多数情况下，建议至少提供源和控制器。 如果要自定义显示，还可以提供表示器。

### <a name="implement-an-intellisense-source"></a>实现 IntelliSense 源
 若要自定义源，您必须实现一个 (或多个以下源接口) ：

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource> 已弃用，以支持 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> 。

 此外，还必须实现相同种类的访问接口：

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider> 已弃用，以支持 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> 。

 必须连同以下属性一起导出提供程序：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：源的名称。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：内容的类型 (例如，源所应用的 "text" 或 "code" ) 。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：源应出现的顺序与其他源)  (相关。

- 下面的示例演示如何在完成源提供程序上导出属性。

```
Export(typeof(ICompletionSourceProvider))]
[Name(" Test Statement Completion Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestCompletionSourceProvider : ICompletionSourceProvider
```

 有关实现 IntelliSense 源的详细信息，请参阅以下演练：

- [演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)

- [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)

### <a name="implement-an-intellisense-controller"></a>实现 IntelliSense 控制器
 若要自定义控制器，必须实现 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> 接口。 此外，还必须实现控制器提供程序以及以下属性：

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：控制器的名称。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>：内容的类型 (例如，控制器适用的 "text" 或 "code" ) 。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>：控制器应出现的顺序与其他控制器)  (相关。

  下面的示例演示如何在完成控制器提供程序上导出特性。

```
Export(typeof(IIntellisenseControllerProvider))]
[Name(" Test Controller Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider
```

 有关使用 IntelliSense 控制器的详细信息，请参阅以下演练：

- [演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)
