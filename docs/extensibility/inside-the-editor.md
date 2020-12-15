---
title: 编辑器内
description: 了解编辑器的子系统和功能。 可以扩展 Visual Studio 编辑器的功能。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 14193c0806c4b45f721ee97b101969de8437448d
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487525"
---
# <a name="inside-the-editor"></a>在编辑器内

编辑器由多个不同的子系统组成，它们旨在使编辑器文本模型与文本视图和用户界面保持分离。

以下各节介绍了该编辑器的不同方面：

- [子系统概述](../extensibility/inside-the-editor.md#overview-of-the-subsystems)

- [文本模型](../extensibility/inside-the-editor.md#the-text-model)

- [文本视图](../extensibility/inside-the-editor.md#the-text-view)

以下部分介绍了该编辑器的功能：

- [标记和分类器](../extensibility/inside-the-editor.md#tags-and-classifiers)

- [修饰](../extensibility/inside-the-editor.md#adornments)

- [投影](../extensibility/inside-the-editor.md#projection)

- [大纲显示](../extensibility/inside-the-editor.md#outlining)

- [鼠标绑定](../extensibility/inside-the-editor.md#mouse-bindings)

- [编辑器操作](../extensibility/inside-the-editor.md#editor-operations)

- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)

## <a name="overview-of-the-subsystems"></a>子系统概述

### <a name="text-model-subsystem"></a>文本模型子系统

文本模型子系统负责表示文本和启用其操作。 文本模型子系统包含 <xref:Microsoft.VisualStudio.Text.ITextBuffer> 接口，该接口描述编辑器要显示的字符序列。 可以通过多种方式修改、跟踪和操作此文本。 文本模型还为以下方面提供了类型：

- 一种服务，它将文本与文件相关联，并管理文件系统中的读取和写入。

- 一种差异服务，用于查找两个对象序列之间的最小差异。

- 用于描述缓冲区中的文本的系统（以其他缓冲区中的文本子集为依据）。

文本模型子系统 (UI) 概念上没有用户界面。 例如，它不负责文本格式设置或文本布局，并且它不知道可能与文本关联的视觉修饰。

文本模型子系统的公共类型包含在 *Microsoft.VisualStudio.Text.Data.dll* 和 *Microsoft.VisualStudio.CoreUtility.dll* 中，后者仅依赖于 .NET Framework 基类库和 Managed Extensibility Framework (MEF) 。

### <a name="text-view-subsystem"></a>文本视图子系统

文本视图子系统负责设置和显示文本格式。 此子系统中的类型划分为两个层，具体取决于这些类型是否依赖于 (WPF) Windows Presentation Foundation。 最重要的类型为 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 和 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> ，它们控制要显示的文本行集，以及使用 WPF UI 元素装饰文本的插入符号、选择和工具。 此子系统还提供文本显示区域周围的边距。 这些边距可以扩展，并且可以包含不同种类的内容和视觉效果。 边距的示例包括行号显示和滚动条。

文本视图子系统的公共类型包含在 *Microsoft.VisualStudio.Text.UI.dll* 和 *Microsoft.VisualStudio.Text.UI.Wpf.dll* 中。 第一个程序集包含独立于平台的元素，第二个程序集包含 WPF 特定的元素。

### <a name="classification-subsystem"></a>分类子系统

分类子系统负责确定文本的字体属性。 分类器将文本分为不同的类，例如 "关键字" 或 "注释"。 分类格式映射将这些类与实际字体属性相关联，例如 "Blue Consolas 10 pt"。 此信息由文本视图在格式化和呈现文本时使用。 标记，本主题后面将对此进行更详细的介绍，使数据与文本范围相关联。

分类子系统的公共类型包含在 Microsoft.VisualStudio.Text.Logic.dll 中，它们与分类的视觉方面进行交互，这些内容包含在 Microsoft.VisualStudio.Text.UI.Wpf.dll 中。

### <a name="operations-subsystem"></a>操作子系统

操作子系统定义编辑器行为。 它提供 Visual Studio 编辑器命令和撤消系统的实现。

## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>更仔细地查看文本模型和文本视图

### <a name="the-text-model"></a>文本模型

文本模型子系统包含不同的文本类型分组。 其中包括文本缓冲区、文本快照和文本跨度。

#### <a name="text-buffers-and-text-snapshots"></a>文本缓冲区和文本快照

<xref:Microsoft.VisualStudio.Text.ITextBuffer>接口表示使用 utf-16 编码的 Unicode 字符序列，这是 .NET Framework 中的类型使用的编码 `String` 。 文本缓冲区可以作为文件系统文档保存，但这不是必需的。

<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>用于创建空文本缓冲区或从字符串或中初始化的文本缓冲区 <xref:System.IO.TextReader> 。 文本缓冲区可作为保存到文件系统 <xref:Microsoft.VisualStudio.Text.ITextDocument> 。

在线程通过调用获得文本缓冲区的所有权之前，任何线程都可以编辑文本缓冲区 <xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A> 。 之后，只有该线程才能执行编辑。

文本缓冲区在其生存期内可以经历许多版本。 每次编辑缓冲区时都会生成一个新版本，并且不变 <xref:Microsoft.VisualStudio.Text.ITextSnapshot> 表示该版本的缓冲区的内容。 由于文本快照是不可变的，因此可以在任何线程上访问文本快照，而无需限制，即使它表示的文本缓冲区继续更改。

#### <a name="text-snapshots-and-text-snapshot-lines"></a>文本快照和文本快照行

可以将文本快照的内容作为字符序列或行序列来查看。 字符和行均从零开始编制索引。 空文本快照包含零个字符和一行。 行由任意有效的 Unicode 换行符序列分隔，或由缓冲区的开头或结尾分隔。 行分隔符在文本快照中显式表示，而文本快照中的换行符并非都必须相同。

> [!NOTE]
> 有关 Visual Studio 编辑器中的分行符的详细信息，请参阅 [编码和分行符](../ide/encodings-and-line-breaks.md)。

文本行由 <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> 对象表示，该对象可从特定行号或特定字符位置的文本快照中获取。

#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>Snapshotpoint、SnapshotSpans 和 NormalizedSnapshotSpanCollections

<xref:Microsoft.VisualStudio.Text.SnapshotPoint>表示快照中的字符位置。 保证位置介于快照的零和长度之间。 <xref:Microsoft.VisualStudio.Text.SnapshotSpan>表示快照中的一段文本。 它的结束位置可以保证介于零和快照的长度之间。 <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>由同一个快照中的一组 <xref:Microsoft.VisualStudio.Text.SnapshotSpan> 对象组成。

#### <a name="spans-and-normalizedspancollections"></a>跨越和 NormalizedSpanCollections

<xref:Microsoft.VisualStudio.Text.Span>表示可应用于文本快照中的一段文本的间隔。 快照位置从零开始，因此，范围可以从任何位置（包括零）开始。 `End`跨度的属性等于其 `Start` 属性及其属性的总和 `Length` 。 不 `Span` 包含由属性编制索引的字符 `End` 。 例如，具有 Start = 5 并且 Length = 3 的跨度的 End = 8，并且它包含位置5、6和7的字符。 此跨度的表示法为 [5. 8) 。

如果两个跨度具有相同的任何位置（包括结束位置），则这两个跨度相交。 因此，[3，5) 和 [2，7) 的交集为 [3，5) ，[3，5) 和 [5，7) 的交集为 [5，5) 。  (注意，[5，5) 为空范围。 ) 

如果两个跨度具有相同的位置，则除了结束位置之外，两个范围重叠。 空跨度决不会与任何其他范围重叠，并且两个范围的重叠不会为空。

是范围的 <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> 列表，它按范围的启动属性顺序排列。 在列表中，重叠或相邻的范围将合并。 例如，如果给定一组跨度 [5.) ，[0. 1) ，[3. 6) ，而 [9.. 10) ，则范围的规范化列表为 [0. 1) ，[3. 10) 。

#### <a name="itextedit-textversion-and-text-change-notifications"></a>ITextEdit、TextVersion 和文本更改通知

可以使用对象更改文本缓冲区的内容 <xref:Microsoft.VisualStudio.Text.ITextEdit> 。 使用) 的方法之一 (创建此类对象将 `CreateEdit()` <xref:Microsoft.VisualStudio.Text.ITextBuffer> 启动由文本编辑组成的文本事务。 每个编辑都是通过字符串替换缓冲区中的某些文本跨度。 启动事务时，每个编辑的坐标和内容均相对于缓冲区的快照表示。 <xref:Microsoft.VisualStudio.Text.ITextEdit>对象调整受同一事务中的其他编辑操作影响的编辑的坐标。

例如，请考虑一个包含此字符串的文本缓冲区：

```
abcdefghij
```

应用包含两个编辑的事务，其中一个编辑将使用字符替换 [2.. 4) 上的跨度，使用字符 `X` 替换 [6. 9) 处的第二个编辑。 `Y` 结果是此缓冲区：

```
abXefYj
```

在应用第一个编辑之前，将根据事务开始时缓冲区的内容计算第二个编辑的坐标。

当 <xref:Microsoft.VisualStudio.Text.ITextEdit> 通过调用对象的方法提交对象时，对缓冲区所做的更改将生效 `Apply()` 。 如果至少有一个非空的编辑，则会创建一个新的， <xref:Microsoft.VisualStudio.Text.ITextVersion> 并会创建一个新的 <xref:Microsoft.VisualStudio.Text.ITextSnapshot> ，并 `Changed` 引发一个事件。 每个文本版本都有不同的文本快照。 文本快照表示编辑事务后文本缓冲区的完整状态，但文本版本仅描述了从一个快照到下一个快照的更改。 通常，文本快照应使用一次，然后将其丢弃，而文本版本必须保持活动状态一段时间。

文本版本包含 <xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection> 。 此集合描述了应用于快照时产生后续快照的更改。 集合中的每个都 <xref:Microsoft.VisualStudio.Text.ITextChange> 包含更改的字符位置、替换的字符串和替换字符串。 用于基本插入的已替换字符串为空，并且在基本删除时替换字符串为空。 规范化集合始终 `null` 适用于最新版本的文本缓冲区。

<xref:Microsoft.VisualStudio.Text.ITextEdit>在任何时候，都只能为文本缓冲区实例化一个对象，而且必须在拥有文本缓冲区 (的线程上执行所有文本编辑（如果已声明所有权) 。 可以通过调用其 `Cancel` 方法或其方法放弃文本编辑 `Dispose` 。

<xref:Microsoft.VisualStudio.Text.ITextBuffer> 还提供 `Insert()` 与 `Delete()` `Replace()` 在接口上找到的方法类似的、和方法 <xref:Microsoft.VisualStudio.Text.ITextEdit> 。 调用这些与创建 <xref:Microsoft.VisualStudio.Text.ITextEdit> 对象、进行类似调用，然后应用编辑的效果相同。

#### <a name="tracking-points-and-tracking-spans"></a>跟踪点和跟踪范围

<xref:Microsoft.VisualStudio.Text.ITrackingPoint>表示文本缓冲区中的字符位置。 如果缓冲区的编辑方式导致字符的位置改变，则跟踪点会随之移动。 例如，如果跟踪点引用缓冲区中的位置10，并且在缓冲区的开头插入5个字符，则跟踪点将引用位置15。 如果插入操作正好精确地出现在跟踪点指示的位置，则其行为取决于其 <xref:Microsoft.VisualStudio.Text.PointTrackingMode> ，它可以是 `Positive` 或 `Negative` 。 如果跟踪模式为正，则跟踪点指的是同一字符，这现在位于插入的末尾。 如果跟踪模式为负数，则跟踪点将引用原始位置的第一个插入字符。 如果删除了跟踪点表示的位置的字符，则跟踪点将移到已删除范围之后的第一个字符。 例如，如果跟踪点引用位于位置5的字符，并且删除位置3到步骤6的字符，则跟踪点将引用位置3处的字符。

<xref:Microsoft.VisualStudio.Text.ITrackingSpan>表示一系列字符，而不只是一个位置。 其行为由其来确定 <xref:Microsoft.VisualStudio.Text.SpanTrackingMode> 。 如果范围跟踪模式为 [SpanTrackingMode. EdgeInclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeInclusive)，则跟踪跨度会增长以合并其边缘处插入的文本。 如果范围跟踪模式为 [SpanTrackingMode. EdgeExclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeExclusive)，则跟踪跨度不会合并在边缘处插入的文本。 但是，如果范围跟踪模式为 [SpanTrackingMode](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgePositive)，则插入会将当前位置推入开头，如果范围跟踪模式为 [SpanTrackingMode](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeNegative)，则插入会将当前位置向末尾推送。

您可以获取跟踪点或其所属文本缓冲区的任何快照的跟踪范围的跨度。 可以从任何线程安全地引用跟踪点和跟踪范围。

#### <a name="content-types"></a>内容类型

内容类型是一种用于定义不同种类的内容的机制。 内容类型可以是文件类型，如 "文本"、"代码" 或 "二进制" 或 "xml"、"vb" 或 "c #" 之类的技术类型。 例如，单词 "using" 是 c # 和 Visual Basic 中的关键字，而不是其他编程语言中的关键字。 因此，此关键字的定义将限制为 "c #" 和 "vb" 内容类型。

内容类型用作修饰和编辑器的其他元素的筛选器。 许多编辑器功能和扩展点按内容类型进行定义。 例如，纯文本文件、XML 文件和 Visual Basic 源代码文件的文本颜色不同。 通常，在创建文本缓冲区时，将为其分配内容类型，并且可以更改文本缓冲区的内容类型。

内容类型可以多个继承自其他内容类型。 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>允许您指定多个基类型作为给定内容类型的父级。

开发人员可以定义自己的内容类型，并使用对其进行注册 <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> 。 对于特定内容类型，可以使用来定义许多编辑器功能 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 。 例如，可以定义编辑器边距、修饰和鼠标处理程序，使其仅应用于显示特定内容类型的编辑器。

### <a name="the-text-view"></a>文本视图

模型视图控制器 (MVC) 模式的视图部分定义文本视图、视图的格式、图形元素（如滚动条）和插入符号。 Visual Studio 编辑器的所有呈现元素都基于 WPF。

#### <a name="text-views"></a>文本视图

<xref:Microsoft.VisualStudio.Text.Editor.ITextView>接口是文本视图的与平台无关的表示形式。 它主要用于在窗口中显示文本文档，但也可用于其他目的，例如，在工具提示中。

文本视图引用不同种类的文本缓冲区。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A>属性指的是 <xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel> 指向这三个不同文本缓冲区的对象：数据缓冲区，数据缓冲区是顶级的数据缓冲区、编辑缓冲区、发生编辑的缓冲区以及显示在文本视图中的缓冲区。

文本基于附加到基础文本缓冲区的分类器进行设置，并使用附加到文本视图本身的修饰提供程序进行装饰。

#### <a name="the-text-view-coordinate-system"></a>文本视图坐标系统

文本视图坐标系统在文本视图中指定位置。 在此坐标系中，x 值0.0 对应于正在显示的文本的左边缘，y 值0.0 对应于要显示的文本的上边缘。 X 坐标从左到右增加，y 坐标从上到下增加。

视区 (在文本窗口中可见) 文本部分在垂直滚动时无法水平滚动。 通过更改视区的左坐标，使其在水平方向上滚动，使其相对于绘图图面移动。 但是，视区只能通过更改呈现的文本来垂直滚动，这将导致 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> 引发事件。

坐标系统中的距离对应于逻辑像素。 如果显示文本呈现图面的情况下没有缩放变换，则文本呈现坐标系统中的一个单元对应于显示的一个像素。

#### <a name="margins"></a>边距

<xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin>接口表示边距，并允许控制边距及其大小的可见性。 有四个预定义的边距，分别名为 "Top"、"左"、"右" 和 "下"，并附加到视图的上、下、左或右边缘。 这些边距是可以在其中放置其他边距的容器。 接口定义返回边距大小和边距可见性的方法。 边距是可视元素，这些元素提供有关其附加到的文本视图的其他信息。 例如，行号边距显示文本视图的行号。 字形边距显示 UI 元素。

<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider>接口处理边距的创建和放置。 可根据其他边距对边距进行排序。 优先级较高的边距更接近文本视图。 例如，如果有两个左边距，边距 A 和边距 B，边距 B 的优先级低于边距 A，则边距 B 显示在边距 A 的左侧。

#### <a name="the-text-view-host"></a>文本视图宿主

该 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> 界面包含文本视图以及该视图附带的任何邻接修饰，例如滚动条。 文本视图宿主还包含附加到视图边框的边距。

#### <a name="formatted-text"></a>带格式文本

文本视图中显示的文本由 <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> 对象组成。 每个文本视图行对应于文本视图中的一行文本。 如果未启用 "自动换行" 功能，则基础文本缓冲区中的长行可以部分遮盖 () 或拆分为多个文本视图行。 此 <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> 接口包含坐标和字符之间的映射方法和属性，以及可能与该行关联的修饰的方法和属性。

<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> 使用接口创建对象 <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> 。 如果你只是想要了解当前在视图中显示的文本，则可以忽略格式设置源。 如果对视图中不显示的文本格式感兴趣 (例如，若要支持 rtf 剪切和粘贴) ，可以使用 <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> 设置文本缓冲区中的文本格式。

文本视图 <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> 一次设置一个。

## <a name="editor-features"></a>编辑器功能

设计编辑器的功能，以使该功能的定义与它的实现分离。 该编辑器包含以下功能：

- 标记和分类器

- 修饰

- 投影

- 大纲显示

- 鼠标和键绑定

- 操作和基元

- IntelliSense

### <a name="tags-and-classifiers"></a>标记和分类器

标记是与文本范围关联的标记。 它们可以以不同的方式显示，例如，使用文本颜色、下划线、图形或弹出窗口。 分类器是一种标记。

其他类型的标记 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 用于文本突出显示、 <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> 大纲显示和 <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> 编译错误。

#### <a name="classification-types"></a>分类类型

<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>接口表示等效类，后者是文本的抽象类别。 分类类型可以多个继承自其他分类类型。 例如，编程语言分类可能包含 "关键字"、"注释" 和 "标识符"，它们都继承自 "代码"。 自然语言分类类型可能包括 "名词"、"动词" 和 "形容词"，它们都继承自 "自然语言"。

#### <a name="classifications"></a>分类

分类是特定分类类型的实例，通常在文本范围内。 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan>用于表示分类。 分类范围可以被视为一个标签，该标签涵盖特定的文本范围，并告知系统此范围的文本属于特定分类类型。

#### <a name="classifiers"></a>分类

<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>是将文本分为一组分类的机制。 必须为特定内容类型定义分类器，并为特定的文本缓冲区实例化分类器。 客户端必须实现 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> 以参与文本分类。

#### <a name="classifier-aggregators"></a>分类器聚合器

分类器聚合器是一种机制，它将一个文本缓冲区的所有分类器组合为一组分类。 例如，c # 分类器和英语分类器均可通过 c # 文件中的注释创建分类。 请看下面的注释：

```
// This method produces a classifier
```

C # 分类器可以将整个范围标记为注释，而英语的分类器可能会将 "生成" 分类为 "谓词"，将 "方法" 归类为 "名词"。 聚合器生成一组非重叠分类，而集的类型基于所有贡献。

分类器聚合器也是分类器，因为它将文本分为一组分类。 分类器聚合器还可确保没有重叠分类并且分类已排序。 单个分类器可随意按任意顺序返回任何分类集，并以任何方式重叠。

#### <a name="classification-formatting-and-text-coloring"></a>分类格式和文本着色

文本格式是基于文本分类构建的功能的一个示例。 文本视图层使用它来确定应用程序中文本的显示。 文本格式设置区域依赖于 WPF，但分类的逻辑定义不依赖于 WPF。

分类格式是特定分类类型的一组格式设置属性。 这些格式继承自分类类型的父项的格式。

<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>是从分类类型到一组文本格式设置属性的映射。 编辑器中的格式映射实现处理分类格式的所有导出。

### <a name="adornments"></a>修饰

修饰是图形效果，与文本视图中字符的字体和颜色无关。 例如，用于标记许多编程语言中的非编译代码的红色波形曲线是嵌入的修饰，而工具提示是弹出式修饰。 修饰派生自 <xref:System.Windows.UIElement> 并实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITag> 。 修饰标记的两个专用类型为 <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> ，用于与视图中的文本占用相同空间的修饰，以及 <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> 用于曲线下划线的修饰。

嵌入的修饰是格式文本视图的一部分的图形。 它们按不同的 Z 顺序分层组织。 有三个内置层，如下所示：文本、插入符号和选择。 但是，开发人员可以定义更多层，并按照彼此的顺序进行排列。 这三种类型的嵌入修饰是文本相关修饰 (它们在文本移动时移动，并在删除文本时被删除) 、视图相对装饰 (与视图的非文本部分) 以及所有者控制的修饰 (开发人员必须管理其放置) 。

弹出式修饰是显示在文本视图上方的小窗口中的图形，如工具提示。

### <a name="projection"></a><a name="projection"></a> 投影

投影是一种方法，用于构造不同类型的文本缓冲区，而不是实际存储文本，而是合并其他文本缓冲区中的文本。 例如，投影缓冲区可用于连接其他两个缓冲区中的文本，并显示结果，就好像它只在一个缓冲区中，或是隐藏一个缓冲区中的部分文本。 投影缓冲区可以充当其他投影缓冲区的源缓冲区。 可以构造一组由投影相关的缓冲区，以多种不同的方式重新排列文本。  (此类集也称为 *缓冲区图*。 ) visual studio 文本大纲显示功能通过使用投影缓冲区隐藏折叠文本来实现，而 visual studio ASP.NET 页面使用投影来支持 Visual Basic 和 c # 等嵌入语言。

<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>使用创建 <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService> 。 投影缓冲区由一系列有序 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 对象（称为 *源范围*）表示。 这些范围中的内容显示为一个字符序列。 从中提取源跨度的文本缓冲区称为 *源缓冲区*。 投影缓冲区的客户端不必知道它不同于普通文本缓冲区。

投影缓冲区侦听源缓冲区中的文本更改事件。 当源范围中的文本更改时，投影缓冲区会将更改的文本坐标映射到其自己的坐标，并引发相应的文本更改事件。 例如，请考虑源缓冲区 A 和 B，其中包含以下内容：

```
A: ABCDE
B: vwxyz
```

如果投影缓冲区 P 由两个文本范围组成，其中一个包含所有缓冲区 A，另一个具有所有缓冲区 B，则 P 具有以下内容：

```
P: ABCDEvwxyz
```

如果 `xy` 从缓冲区 B 中删除子字符串，则 Buffer P 将引发一个事件，该事件指示已删除位置7和8处的字符。

还可以直接编辑投影缓冲区。 它将编辑传播到适当的源缓冲区。 例如，如果将字符串插入到缓冲区 P 中的位置 6 (字符 "v" ) 的原始位置，则会将插入量传播到缓冲区 B 的位置1。

对投影缓冲区产生影响的源范围存在限制。 源跨度可能不重叠;投影缓冲区中的某个位置无法映射到任何源缓冲区中的多个位置，并且源缓冲区中的某个位置无法映射到投影缓冲区中的多个位置。 源缓冲关系中不允许 circularities。

当投影缓冲区的一组源缓冲区更改时以及源范围的集合发生更改时，将引发事件。
省略缓冲区是一种特殊的投影缓冲区。 它主要用于大纲显示以及展开和折叠文本块的操作。 省略缓冲区仅基于一个源缓冲区，并且省略缓冲区中的范围必须按其在源缓冲区中的顺序排列。

#### <a name="the-buffer-graph"></a>缓冲区图形

使用 <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph> 接口可以在投影缓冲区图形之间进行映射。 所有文本缓冲区和投影缓冲区均以定向非循环图形的形式收集，这与语言编译器生成的抽象语法树非常类似。 关系图由顶部缓冲区定义，可以是任何文本缓冲区。 缓冲区关系图可以将顶部缓冲区中的某个点映射到源缓冲区中的某个点，或映射到源缓冲区中的一组范围内的顶部缓冲区中的某个点。 同样，它可以将一个点或范围从源缓冲区映射到顶部缓冲区中的某个点。 缓冲区图形是使用创建的 <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService> 。

#### <a name="events-and-projection-buffers"></a>事件和投影缓冲区

当修改投影缓冲区时，会将修改从投影缓冲区发送到依赖于它的缓冲区。 在修改所有缓冲区后，将从最深的缓冲区开始引发缓冲区更改事件。

### <a name="outlining"></a>大纲显示

大纲显示可以在文本视图中展开或折叠不同文本块。 大纲定义为一种类型的 <xref:Microsoft.VisualStudio.Text.Tagging.ITag> ，与修饰的定义方式相同。 <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>是一个标记，用于定义可展开或折叠的文本区域。 若要使用大纲显示，您必须导入 <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService> 以获取 <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> 。 大纲显示管理器枚举、折叠和展开不同的块（表示为 <xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible> 对象），并相应地引发事件。

### <a name="mouse-bindings"></a>鼠标绑定

鼠标绑定将鼠标移动到不同的命令。 鼠标绑定是通过使用定义的 <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> ，键绑定是使用定义的 <xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider> 。 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>自动实例化所有绑定，并将其连接到视图中的鼠标事件。

<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor>接口包含用于不同鼠标事件的预处理后处理事件处理程序。 若要处理某个事件，可以重写中的某些方法 <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> 。

### <a name="editor-operations"></a>编辑器操作

编辑器操作可用于自动与编辑器交互，以实现脚本或其他目的。 您可以导入 <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService> 到给定的上的访问操作 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。 然后，可以使用这些对象修改所选内容，滚动视图，或将插入符号移动到视图的不同部分。

### <a name="intellisense"></a>IntelliSense

IntelliSense 支持语句完成、签名帮助 (也称为参数信息) 、快速信息和浅电灯泡。

语句完成为方法名称、XML 元素以及其他编码或标记元素提供可能的完成的弹出列表。 通常，用户笔势调用完成会话。 该会话将显示可能的完成的列表，用户可以选择一个列表或取消列表。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>负责创建和触发 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession> 。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>计算会话的 <xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet> 完成项的。

## <a name="see-also"></a>请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [编辑器导入](../extensibility/editor-imports.md)
