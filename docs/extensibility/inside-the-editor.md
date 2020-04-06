---
title: 编辑器内
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - architecture
ms.assetid: 822cbb8d-7ab4-40ee-bd12-44016ebcce81
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bba0b5192df53b6ec837b0030c7b236bf8e08dea
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710316"
---
# <a name="inside-the-editor"></a>编辑器内部

编辑器由几个不同的子系统组成，这些子系统旨在使编辑器文本模型与文本视图和用户界面分开。

这些部分描述了编辑器的不同方面：

- [子系统概述](../extensibility/inside-the-editor.md#overview-of-the-subsystems)

- [文本模型](../extensibility/inside-the-editor.md#the-text-model)

- [文本视图](../extensibility/inside-the-editor.md#the-text-view)

这些部分描述了编辑器的功能：

- [标记和分类器](../extensibility/inside-the-editor.md#tags-and-classifiers)

- [装饰品](../extensibility/inside-the-editor.md#adornments)

- [投影](../extensibility/inside-the-editor.md#projection)

- [大纲显示](../extensibility/inside-the-editor.md#outlining)

- [鼠标绑定](../extensibility/inside-the-editor.md#mouse-bindings)

- [编辑器操作](../extensibility/inside-the-editor.md#editor-operations)

- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)

## <a name="overview-of-the-subsystems"></a>子系统概述

### <a name="text-model-subsystem"></a>文本模型子系统

文本模型子系统负责表示文本并启用其操作。 文本模型子系统包含<xref:Microsoft.VisualStudio.Text.ITextBuffer>接口，该接口描述编辑器要显示的字符序列。 可以通过多种方式修改、跟踪或以其他方式操作此文本。 文本模型还提供以下方面的类型：

- 将文本与文件关联，并在文件系统中管理读取和写入这些文件的服务。

- 一种不同的服务，它查找两个对象序列之间的最小差异。

- 一种系统，用于根据其他缓冲区中文本的子集在缓冲区中描述文本。

文本模型子系统没有用户界面 （UI） 概念。 例如，它不负责文本格式或文本布局，并且不了解可能与文本关联的可视修饰。

文本模型子系统的公共类型包含在*Microsoft.VisualStudio.Text.Data.dll*和*Microsoft.VisualStudio.CoreUtility.dll 中*，它们仅依赖于 .NET 框架基类库和托管扩展性框架 （MEF）。

### <a name="text-view-subsystem"></a>文本视图子系统

文本视图子系统负责设置文本的格式和显示。 此子系统中的类型分为两层，具体取决于类型是否依赖于 Windows 演示文稿基础 （WPF）。 最重要的类型是<xref:Microsoft.VisualStudio.Text.Editor.ITextView>和<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>，它控制要显示的文本行集，以及使用 WPF UI 元素进行修饰文本的加注、选择和修饰文本的设施。 此子系统还提供文本显示区域周围的边距。 这些边距可以扩展，并可以包含不同类型的内容和视觉效果。 边距的示例包括行号显示和滚动条。

文本视图子系统的公共类型包含在*Microsoft.VisualStudio.Text.UI.dll*和*Microsoft.VisualStudio.Text.UI.Wpf.dll 中*。 第一个程序集包含与平台无关的元素，第二个程序集包含特定于 WPF 的元素。

### <a name="classification-subsystem"></a>分类子系统

分类子系统负责确定文本的字体属性。 分类器将文本分成不同的类，例如"关键字"或"注释"。 分类格式映射将这些类与实际字体属性相关联，例如"蓝色 Consolas 10 pt"。 文本视图在设置文本格式和呈现文本时使用此信息。 在本主题的后面部分介绍的标记使数据能够与文本范围相关联。

分类子系统的公共类型包含在 Microsoft.VisualStudio.Text.Logic.dll 中，它们与 Microsoft.VisualStudio.Text.UI.Wpf.dll 中包含的分类的可视方面进行交互。

### <a name="operations-subsystem"></a>操作子系统

操作子系统定义编辑器行为。 它为 Visual Studio 编辑器命令和撤消系统提供了实现。

## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>仔细查看文本模型和文本视图

### <a name="the-text-model"></a>文本模型

文本模型子系统由不同的文本类型分组组成。 其中包括文本缓冲区、文本快照和文本范围。

#### <a name="text-buffers-and-text-snapshots"></a>文本缓冲区和文本快照

该<xref:Microsoft.VisualStudio.Text.ITextBuffer>接口表示使用 UTF-16 编码的 Unicode 字符序列，UTF-16 是`String`.NET 框架中的类型使用的编码。 文本缓冲区可以保留为文件系统文档，但这不是必填项。

<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>用于创建空文本缓冲区或从字符串或 初始<xref:System.IO.TextReader>化的文本缓冲区。 文本缓冲区可以作为 保存到文件系统<xref:Microsoft.VisualStudio.Text.ITextDocument>。

任何线程都可以编辑文本缓冲区，直到线程通过调用<xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A>获取文本缓冲区的所有权。 之后，只有该线程可以执行编辑。

文本缓冲区在其生存期内可以遍遍多个版本。 每次编辑缓冲区时都会生成新版本，并且不可变<xref:Microsoft.VisualStudio.Text.ITextSnapshot>表示该缓冲区版本的内容。 由于文本快照是不可变的，因此即使文本快照继续更改，也可以不受限制地访问任何线程上的文本快照。

#### <a name="text-snapshots-and-text-snapshot-lines"></a>文本快照和文本快照行

您可以将文本快照的内容视为字符序列或行序列。 字符和行都从零开始编制索引。 空文本快照包含零个字符和一行空行。 行由任何有效的 Unicode 换行字符序列或缓冲区的开头或结尾分隔。 换行符在文本快照中显式表示，文本快照中的换行符不一定全部相同。

> [!NOTE]
> 有关 Visual Studio 编辑器中换行符的详细信息，请参阅[编码和换行](../ide/encodings-and-line-breaks.md)符 。

文本行由对象<xref:Microsoft.VisualStudio.Text.ITextSnapshotLine>表示，可以从特定行号或特定字符位置的文本快照获取该对象。

#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>快照点、快照范围和规范化快照跨集合

表示<xref:Microsoft.VisualStudio.Text.SnapshotPoint>快照中的字符位置。 该位置保证位于零和快照长度之间。 表示<xref:Microsoft.VisualStudio.Text.SnapshotSpan>快照中的文本范围。 其结束位置保证位于零和快照长度之间。 由<xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>同一快照中的<xref:Microsoft.VisualStudio.Text.SnapshotSpan>一组对象组成。

#### <a name="spans-and-normalizedspancollections"></a>跨和标准化跨值集合

表示<xref:Microsoft.VisualStudio.Text.Span>可应用于文本快照中的文本范围的间隔。 快照位置是零基的，因此范围可以从任何位置开始，包括零。 范围`End`的属性等于其`Start`属性及其`Length`属性的总和。 `Span`不包括由 属性索引的`End`字符。 例如，具有 Start=5 和 Length=3 的跨距具有 End=8，并且它包括位置 5、6 和 7 处的字符。 此跨度的表示法为 [5...8）。

如果两个跨段具有任何共同位置（包括结束位置），则它们相交。 因此，[3， 5） 和 #2， 7） 的交点为 [3， 5） 和 [5， 7） 的交点为 [5， 5）。 （请注意，[5， 5） 是一个空跨度。

两个跨距重叠，如果它们具有共同位置，则"结束"位置除外。 空范围永远不会重叠任何其他范围，并且两个范围的重叠永远不会为空。

A<xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection>是跨范围的"开始"属性的顺序的跨范围列表。 在列表中，重叠或对头跨度合并。 例如，给定范围集 [5...9"、"0..1"、"{3..6]和 [9..10），规范化范围列表为 [0..1][3..10] 。

#### <a name="itextedit-textversion-and-text-change-notifications"></a>IText 编辑、文本版本和文本更改通知

可以使用<xref:Microsoft.VisualStudio.Text.ITextEdit>对象更改文本缓冲区的内容。 创建此类对象（通过使用`CreateEdit()`<xref:Microsoft.VisualStudio.Text.ITextBuffer>的方法之一）将启动由文本编辑组成的文本事务。 每次编辑都会将缓冲区中的某些文本跨度由字符串替换。 每次编辑的坐标和内容都相对于启动事务时缓冲区的快照表示。 对象<xref:Microsoft.VisualStudio.Text.ITextEdit>调整受同一事务中其他编辑影响的编辑的坐标。

例如，请考虑包含此字符串的文本缓冲区：

```
abcdefghij
```

应用包含两个编辑的事务，一个编辑使用字符`X`替换范围在 {2..4），第二个编辑使用字符`Y`替换范围在 {6..9} 结果是此缓冲区：

```
abXefYj
```

在应用第一次编辑之前，针对事务开头的缓冲区内容计算第二个编辑的坐标。

当通过调用其<xref:Microsoft.VisualStudio.Text.ITextEdit>`Apply()`方法提交对象时，对缓冲区的更改将生效。 如果至少有一个非空编辑，则创建一个新<xref:Microsoft.VisualStudio.Text.ITextVersion>编辑，创建一个新<xref:Microsoft.VisualStudio.Text.ITextSnapshot>编辑，并引发一个`Changed`事件。 每个文本版本都有不同的文本快照。 文本快照表示编辑事务后文本缓冲区的完整状态，但文本版本仅描述从一个快照到下一个快照的更改。 通常，文本快照要使用一次，然后丢弃，而文本版本必须保持一段时间的处于活动状态。

文本版本包含 。 <xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection> 此集合描述应用于快照时生成后续快照的更改。 集合<xref:Microsoft.VisualStudio.Text.ITextChange>中的每个成员都包含更改的字符位置、替换的字符串和替换字符串。 替换的字符串对于基本插入为空，替换字符串为空，用于基本删除。 规范化集合始终`null`用于最新版本的文本缓冲区。

任何时候都只能<xref:Microsoft.VisualStudio.Text.ITextEdit>实例化一个对象的文本缓冲区，并且所有文本编辑都必须在拥有文本缓冲区的线程上执行（如果已声明所有权）。 可以通过调用文本`Cancel`编辑的方法或方法`Dispose`来放弃文本编辑。

<xref:Microsoft.VisualStudio.Text.ITextBuffer>还提供了`Insert()``Delete()`与`Replace()`<xref:Microsoft.VisualStudio.Text.ITextEdit>接口上找到的方法类似的 方法。 调用这些具有与创建<xref:Microsoft.VisualStudio.Text.ITextEdit>对象、进行类似调用以及然后应用编辑相同的效果。

#### <a name="tracking-points-and-tracking-spans"></a>跟踪点和跟踪范围

表示<xref:Microsoft.VisualStudio.Text.ITrackingPoint>文本缓冲区中的字符位置。 如果以导致字符位置移动的方式编辑缓冲区，则跟踪点将随其移动。 例如，如果跟踪点引用缓冲区中的位置 10，并且在缓冲区的开头插入五个字符，则跟踪点则引用位置 15。 如果插入发生在跟踪点表示的位置，则其行为由 其<xref:Microsoft.VisualStudio.Text.PointTrackingMode>决定，可以是 或`Positive``Negative`。 如果跟踪模式为正，则跟踪点引用同一字符，该字符现在位于插入的末尾。 如果跟踪模式为负，则跟踪点是指原始位置的第一个插入字符。 如果删除跟踪点表示的位置的字符，则跟踪点将转移到删除范围后的第一个字符。 例如，如果跟踪点引用位置 5 处的字符，并且位置 3 到 6 处的字符被删除，则跟踪点引用位置 3 处的字符。

表示<xref:Microsoft.VisualStudio.Text.ITrackingSpan>一系列字符，而不是仅表示一个位置。 其行为由 其<xref:Microsoft.VisualStudio.Text.SpanTrackingMode>决定。 如果跨距跟踪模式为[SpanTrackingMode.Edge包容](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeInclusive)，则跟踪范围将增大以合并插入在其边缘的文本。 如果跨距跟踪模式为[SpanTrackIngMode.EdgeExclusive，](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeExclusive)则跟踪范围不包含插入在其边缘的文本。 但是，如果跨距跟踪模式为["跨跟踪模式.Edge积极](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgePositive)"，则插入会将当前位置推向起始位置，如果跨距跟踪模式为["跨跟踪模式.Edge 负"，](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeNegative)则插入将当前位置推向末端。

您可以获取跟踪点的位置或跟踪范围的范围，用于它们所属的文本缓冲区的任何快照。 跟踪点和跟踪范围可以从任何线程安全地引用。

#### <a name="content-types"></a>内容类型

内容类型是定义不同类型的内容的机制。 内容类型可以是文件类型，如"文本"、"代码"或"二进制"，也可以是技术类型（如"xml"、"vb"或"c#"。）。 例如，"使用"一词是 C# 和 Visual Basic 中的关键字，但在其他编程语言中则不是关键字。 因此，此关键字的定义将仅限于"c#"和"vb"内容类型。

内容类型用作编辑器的修饰和其他元素的筛选器。 许多编辑器功能和扩展点都是根据内容类型定义的。 例如，纯文本文件、XML 文件和 Visual Basic 源代码文件的文本着色是不同的。 文本缓冲区通常在创建时分配内容类型，并且可以更改文本缓冲区的内容类型。

内容类型可以从其他内容类型进行多次继承。 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>允许您将多个基类型指定为给定内容类型的父类型。

开发人员可以定义自己的内容类型，并使用 注册<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>它们。 可以使用 来定义许多编辑器功能相对于特定内容类型<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>。 例如，可以定义编辑器边距、修饰和鼠标处理程序，以便它们仅适用于显示特定内容类型的编辑器。

### <a name="the-text-view"></a>文本视图

模型视图控制器 （MVC） 模式的视图部分定义文本视图、视图的格式、图形元素（如滚动条）和图。 可视化工作室编辑器的所有表示元素都基于 WPF。

#### <a name="text-views"></a>文本视图

该<xref:Microsoft.VisualStudio.Text.Editor.ITextView>接口是文本视图与平台无关的表示形式。 它主要用于在窗口中显示文本文档，但也可用于其他目的，例如工具提示中。

文本视图引用不同类型的文本缓冲区。 该<xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A>属性引用指向<xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel>这三个不同的文本缓冲区的对象：数据缓冲区（即顶部数据级缓冲区）、编辑缓冲区（其中进行编辑）和可视缓冲区（文本视图中显示的缓冲区）。

文本基于附加到基础文本缓冲区的分类器进行格式化，并使用附加到文本视图本身的修饰提供程序进行修饰。

#### <a name="the-text-view-coordinate-system"></a>文本视图坐标系

文本视图坐标系指定文本视图中的位置。 在此坐标系中，x 值 0.0 对应于显示的文本的左边缘，y 值 0.0 对应于显示的文本的上边缘。 x 坐标从左到右增加，y 坐标从上到下增加。

视口（文本窗口中可见的文本部分）不能以与垂直滚动相同的水平方式滚动。 视口通过更改其左侧坐标水平滚动，以便相对于绘图曲面移动。 但是，只能通过更改呈现的文本垂直滚动视口，从而导致引发<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>事件。

坐标系中的距离对应于逻辑像素。 如果文本呈现曲面在没有缩放变换的情况下显示，则文本呈现坐标系中的一个单位对应于显示屏上的一个像素。

#### <a name="margins"></a>边距

接口<xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin>表示边距，并能够控制边距的可见性及其大小。 有四个预定义的边距，分别命名为"顶部"、"左侧"、"右侧"和"底部"，并附加到视图的顶部、底部、左侧或右边缘。 这些边距是可以放置其他边距的容器。 接口定义返回边距大小和边距可见性的方法。 边距是可视元素，提供有关它们附加到的文本视图的其他信息。 例如，行号边距显示文本视图的行号。 字形边距显示 UI 元素。

接口<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider>处理边距的创建和放置。 边距可以相对于其他边距进行排序。 优先级较高的边距位于更接近文本视图的位置。 例如，如果有两个边距，边距 A 和边距 B，并且边距 B 的优先级低于边距 A，则边距 B 将显示在边距 A 的左侧。

#### <a name="the-text-view-host"></a>文本视图主机

界面<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>包含文本视图和伴随视图的任何边装饰，例如滚动条。 文本视图主机还包含附加到视图边框的边距。

#### <a name="formatted-text"></a>带格式文本

文本视图中显示的文本由<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>对象组成。 每个文本视图行对应于文本视图中的一行文本。 基础文本缓冲区中的长行可以部分遮盖（如果未启用换行字），也可以分成多个文本视图行。 接口<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>包含用于在坐标和字符之间映射的方法和属性，以及可能与行关联的修饰。

<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>对象是使用<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>接口创建的。 如果您只关注视图中当前显示的文本，则可以忽略格式源。 如果您对视图中未显示的文本格式感兴趣（例如，为了支持富文本剪切和粘贴），则可以使用在<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>文本缓冲区中设置文本的格式。

文本视图一次设置<xref:Microsoft.VisualStudio.Text.ITextSnapshotLine>一个格式。

## <a name="editor-features"></a>编辑器功能

编辑器的功能的设计是为了让要素的定义与其实现分开。 编辑器包括以下功能：

- 标记和分类器

- 装饰品

- 投影

- 大纲显示

- 鼠标和密钥绑定

- 操作和基元

- IntelliSense

### <a name="tags-and-classifiers"></a>标记和分类器

标记是与文本范围关联的标记。 它们可以以不同的方式呈现，例如，通过使用文本着色、下划线、图形或弹出窗口。 分类器是一种标记。

其他类型的标记用于<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>文本突出显示、<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>大纲和<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>编译错误。

#### <a name="classification-types"></a>分类类型

接口<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>表示等价类，它是文本的抽象类别。 分类类型可以从其他分类类型进行多重继承。 例如，编程语言分类可能包括"关键字"、"注释"和"标识符"，它们都从"代码"继承。 自然语言分类类型可能包括"名词"、"动词"和"形容词"，它们都从"自然语言"中继承。

#### <a name="classifications"></a>分类

分类是特定分类类型的实例，通常跨越文本范围。 A<xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan>表示分类。 分类范围可以视为涵盖特定文本范围并告诉系统此文本范围为特定分类类型的标签。

#### <a name="classifiers"></a>分类

<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>是一种将文本分解为一组分类的机制。 必须为特定内容类型定义分类器，并为特定文本缓冲区实例化分类。 客户端必须实现<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>才能参与文本分类。

#### <a name="classifier-aggregators"></a>分类器聚合器

分类器聚合器是一种机制，它将一个文本缓冲区的所有分类器合并为一组分类。 例如，C# 分类器和英语语言分类器都可以在 C# 文件中的注释上创建分类。 请考虑此注释：

```
// This method produces a classifier
```

C# 分类器可能会将整个范围标记为注释，而英语语言分类器可能会将"生成"归类为"动词"和"方法"为"名词"。 聚合器生成一组非重叠分类，并且该集合的类型基于所有贡献。

分类器聚合器也是分类器，因为它将文本分解为一组分类。 分类器聚合器还确保没有重叠的分类，并且对分类进行排序。 各个分类器可以按任意顺序自由返回任何分类集，并以任何方式重叠。

#### <a name="classification-formatting-and-text-coloring"></a>分类格式和文本着色

文本格式是基于文本分类构建的功能的示例。 文本视图层使用它来确定应用程序中的文本显示。 文本格式区域取决于 WPF，但分类的逻辑定义不。

分类格式是特定分类类型的一组格式设置属性。 这些格式从分类类型的父格式继承。

是从<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>分类类型映射到一组文本格式属性。 编辑器中格式映射的实现处理分类格式的所有导出。

### <a name="adornments"></a>装饰品

装饰是与文本视图中字符的字体和颜色没有直接关系的图片效果。 例如，用于标记许多编程语言中非编译代码的红色波浪线下划线是一种嵌入的修饰，工具提示是弹出式修饰。 修饰派生自<xref:System.Windows.UIElement>和实现<xref:Microsoft.VisualStudio.Text.Tagging.ITag>。 两种专用类型的修饰标记是<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>，对于占据与视图中文本相同的空间的修饰，以及<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>用于波浪线下划线。

嵌入修饰是构成格式化文本视图一部分的图形。 它们以不同的 Z 顺序图层组织。 有三个内置图层，如下所示：文本、加斯特和选择。 但是，开发人员可以定义更多的图层，并使它们彼此有序。 三种嵌入修饰是文本相对修饰（在文本移动时移动，删除文本时删除）、视图相对修饰（与视图的非文本部分有关）和所有者控制的修饰（开发人员必须管理其放置）。

弹出窗口修饰是显示在文本视图上方的小窗口中的图形，例如工具提示。

### <a name="projection"></a><a name="projection"></a>投影

投影是一种构造不同类型的文本缓冲区的技术，该缓冲区实际上不存储文本，而是合并来自其他文本缓冲区的文本。 例如，投影缓冲区可用于从另外两个缓冲区串联文本，并将结果呈现为仅位于一个缓冲区中，或将文本的某些部分隐藏在一个缓冲区中。 投影缓冲区可以充当另一个投影缓冲区的源缓冲区。 可以构造一组由投影相关的缓冲区，以以许多不同的方式重新排列文本。 （这样的集也称为*缓冲区图*。Visual Studio 文本大纲功能通过使用投影缓冲区来隐藏折叠的文本而实现，而 ASP.NET页的 Visual Studio 编辑器使用投影来支持嵌入的语言，如视觉基础和 C#。

使用<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>创建 者<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>使用 。 投影缓冲区由称为<xref:Microsoft.VisualStudio.Text.ITrackingSpan>*源范围*的对象的有序序列表示。 这些范围的内容以字符序列的形式呈现。 从中绘制源范围的文本缓冲区名为*源缓冲区*。 投影缓冲区的客户端不必知道它与普通文本缓冲区不同。

投影缓冲区侦听源缓冲区上的文本更改事件。 当源范围中的文本发生更改时，投影缓冲区将更改的文本坐标映射到其自己的坐标，并引发相应的文本更改事件。 例如，请考虑具有以下内容的源缓冲区 A 和 B：

```
A: ABCDE
B: vwxyz
```

如果投影缓冲区 P 由两个文本范围组成，一个具有缓冲区 A 的所有缓冲区，另一个具有所有缓冲区 B，则 P 具有以下内容：

```
P: ABCDEvwxyz
```

如果子字符串`xy`从缓冲区 B 中删除，则缓冲区 P 将引发一个事件，指示位置 7 和 8 处的字符已被删除。

投影缓冲区也可以直接编辑。 它将编辑传播到相应的源缓冲区。 例如，如果将字符串插入到位置 6 处（字符"v"的原始位置）的缓冲区 P 中，则插入将传播到位置 1 处的缓冲区 B。

源范围存在导致投影缓冲区的限制。 源范围不能重叠;因此，源范围不能重叠。投影缓冲区中的位置不能映射到任何源缓冲区中的多个位置，并且源缓冲区中的位置不能映射到投影缓冲区中的多个位置。 源缓冲区关系中不允许循环。

当投影缓冲区的源缓冲区集发生更改和源范围集更改时，将引发事件。
除去缓冲区是一种特殊的投影缓冲区。 它主要用于大纲和扩展和折叠文本块的操作。 消除缓冲区仅基于一个源缓冲区，并且除功能化缓冲区中的范围必须按在源缓冲区中排序的相同。

#### <a name="the-buffer-graph"></a>缓冲区图

该<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>接口支持跨投影缓冲区的图形进行映射。 所有文本缓冲区和投影缓冲区都收集到定向的循环图中，与语言编译器生成的抽象语法树类似。 图形由顶部缓冲区定义，它可以是任何文本缓冲区。 缓冲区图可以从顶部缓冲区中的点映射到源缓冲区中的点，或者从顶部缓冲区中的范围映射到源缓冲区中的一组范围。 同样，它可以将点或范围从源缓冲区映射到顶部缓冲区中的点。 使用 创建缓冲区图时，将使用<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>。

#### <a name="events-and-projection-buffers"></a>事件和投影缓冲区

修改投影缓冲区时，修改将从投影缓冲区发送到依赖于它的缓冲区。 修改所有缓冲区后，将引发缓冲区更改事件，从最深的缓冲区开始。

### <a name="outlining"></a>大纲显示

大纲是展开或折叠文本视图中不同文本块的能力。 大纲被定义为一种<xref:Microsoft.VisualStudio.Text.Tagging.ITag>，其方式与定义修饰的方式相同。 是<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>定义可以展开或折叠的文本区域的标记。 要使用大纲，必须导入<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>才能获取 。 <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> 大纲管理器枚举、折叠和展开不同的块（表示为<xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible>对象），并相应地引发事件。

### <a name="mouse-bindings"></a>鼠标绑定

鼠标绑定将鼠标移动链接到不同的命令。 鼠标绑定通过使用<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider>定义，键绑定通过使用 定义<xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider>。 自动<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>实例化所有绑定，并将它们连接到视图中的鼠标事件。

该<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor>接口包含不同鼠标事件的预处理和后处理事件处理程序。 要处理其中一个事件，可以重写 中的<xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase>一些方法。

### <a name="editor-operations"></a>编辑器操作

编辑器操作可用于自动与编辑器交互，用于脚本或其他目的。 可以导入<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>以访问给定<xref:Microsoft.VisualStudio.Text.Editor.ITextView>上的操作。 然后，可以使用这些对象修改选择、滚动视图或将图斯特移动到视图的不同部分。

### <a name="intellisense"></a>IntelliSense

IntelliSense 支持语句完成、签名帮助（也称为参数信息）、快速信息和灯泡。

语句完成提供方法名称、XML 元素和其他编码或标记元素的潜在完成列表。 通常，用户手势调用完成会话。 会话显示潜在完成的列表，用户可以选择一个或关闭列表。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>负责创建和触发<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。 计算<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>会话<xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet>的完成项。

## <a name="see-also"></a>请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [编辑器导入](../extensibility/editor-imports.md)
