---
title: 在编辑器内 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - architecture
ms.assetid: 822cbb8d-7ab4-40ee-bd12-44016ebcce81
caps.latest.revision: 32
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8dfc751b040bd775c3f55ff7db804c2a16d45d5f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63414619"
---
# <a name="inside-the-editor"></a>编辑器内
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器是组合多个不同的子系统，旨在使编辑器文本模型单独从文本视图和用户界面。  
  
 下列各节介绍编辑器中的不同的方面：  
  
- [子系统概述](../extensibility/inside-the-editor.md#overview)  
  
- [文本模型](../extensibility/inside-the-editor.md#textmodel)  
  
- [文本视图](../extensibility/inside-the-editor.md#textview)  
  
  这些部分介绍了在编辑器的功能：  
  
- [标记和分类器](../extensibility/inside-the-editor.md#tagsandclassifiers)  
  
- [修饰](../extensibility/inside-the-editor.md#adornments)  
  
- [投影](../extensibility/inside-the-editor.md#projection)  
  
- [大纲显示](../extensibility/inside-the-editor.md#outlining)  
  
- [鼠标绑定](../extensibility/inside-the-editor.md#mousebindings)  
  
- [编辑器操作](../extensibility/inside-the-editor.md#editoroperations)  
  
- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)  
  
## <a name="overview"></a> 子系统概述  
  
### <a name="text-model-subsystem"></a>文本模型子系统  
 文本模型子系统负责表示文本和启用其操作。 文本模型子系统包含<xref:Microsoft.VisualStudio.Text.ITextBuffer>接口，其中描述了通过在编辑器中显示的字符序列。 此文本可以修改、 跟踪，和其他操作在许多方面。 文本模型还提供用于以下方面的类型：  
  
- 将文本相关联的文件，并管理读取和写入这些文件系统中的服务。  
  
- 一种差异服务所发现的对象的两个序列之间的最小差异。  
  
- 用于描述方面的其他缓冲区中的文本子集的缓冲区中的文本的系统。  
  
  文本模型子系统是免费的用户界面 (UI) 概念。 例如，不负责设置文本格式或文本布局，它并不知道可能与文本相关联的 visual 修饰。  
  
  Microsoft.VisualStudio.Text.Data.dll 和 Microsoft.VisualStudio.CoreUtilitiy.dll，只能依赖于.NET Framework 基类库和 Managed Extensibility Framework (MEF) 中包含文本模型子系统的公共类型。  
  
### <a name="text-view-subsystem"></a>文本视图子系统  
 文本视图子系统负责设置格式并显示文本。 此子系统中的类型分为两个层，具体取决于是否类型依赖于 Windows Presentation Foundation (WPF)。 最重要的类型是<xref:Microsoft.VisualStudio.Text.Editor.ITextView>和<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>，用于控制要显示的文本行集和还将插入符号、 选择和用于通过使用 WPF UI 元素装饰文本的功能。 此子系统还提供了文本周围的边距显示区域。 这些边距可加以扩展，并且可以包含不同类型的内容和可视化效果。 边距的示例包括行号显示和滚动条。  
  
 Microsoft.VisualStudio.Text.UI.dll 和 Microsoft.VisualStudio.Text.UI.Wpf.dll 中包含的文本视图子系统的公共类型。 第一个程序集包含独立于平台的元素，并第二个包含特定于 WPF 的元素。  
  
### <a name="classification-subsystem"></a>分类子系统  
 分类子系统负责确定文本的字体属性。 分类器将文本分解为不同的类，例如，"关键字"或"注释"。 分类格式映射到实际的字体属性与这些类，如"蓝色 Consolas 10 磅"。 格式和呈现文本时，文本视图使用此信息。 标记，在本主题后面的更多详细信息中所述使数据能够与跨文本相关联。  
  
 分类子系统的公共类型都包含在 Microsoft.VisualStudio.Text.Logic.dll，并且它们与分类，可视方面，它包含在 Microsoft.VisualStudio.Text.UI.Wpf.dll 进行交互。  
  
### <a name="operations-subsystem"></a>操作子系统  
 操作子系统定义编辑器行为。 它提供了 Visual Studio 编辑器命令的实现和撤消系统。  
  
## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>进一步了解文本模型和文本视图  
  
### <a name="textmodel"></a> 文本模型  
 文本模型子系统包含不同的文本类型分组。 其中包括文本缓冲区、 文本快照和文本段。  
  
#### <a name="text-buffers-and-text-snapshots"></a>文本缓冲区和文本快照  
 <xref:Microsoft.VisualStudio.Text.ITextBuffer>接口表示使用 utf-16，这是编码使用编码的 Unicode 字符序列`String`.NET Framework 中的类型。 文本缓冲区可以保存为文件系统文档，但这不是必需。  
  
 <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>用于创建一个空文本缓冲区或从字符串或从已初始化的文本缓冲区<xref:System.IO.TextReader>。 文本缓冲区可以保存到文件系统作为<xref:Microsoft.VisualStudio.Text.ITextDocument>。  
  
 文本缓冲区可以编辑由任何线程，直到一个线程通过调用采用的文本缓冲区所有权<xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A>。 之后，只有该线程可以执行编辑。  
  
 文本缓冲区可在其生存期内经历许多版本。 新版本生成每次编辑缓冲区，和一个不可变<xref:Microsoft.VisualStudio.Text.ITextSnapshot>表示该版本的缓冲区的内容。 由于文本快照是不可变，您可以访问任何线程，而没有限制的文本快照，即使它表示的文本缓冲区不断变化。  
  
#### <a name="text-snapshots-and-text-snapshot-lines"></a>文本快照和文本快照行  
 作为一系列字符或一系列行，可以查看文本快照的内容。 字符和行都是同时索引从零开始。 空文本快照包含零个字符和一个空的行。 由任何有效 Unicode 换行字符序列，或开始或缓冲区末尾的分隔行。 换行字符显式表示文本快照中并不是所有具有相同文本快照中的换行。  
  
> [!NOTE]
> 有关 Visual Studio 编辑器中的换行字符的详细信息，请参阅[编码和换行符](../ide/encodings-and-line-breaks.md)。  
  
 表示文本行<xref:Microsoft.VisualStudio.Text.ITextSnapshotLine>对象，可以获取从文本快照的特定行数或特定的字符位置。  
  
#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>Snapshotpoint、 SnapshotSpans 和 NormalizedSnapshotSpanCollections  
 一个<xref:Microsoft.VisualStudio.Text.SnapshotPoint>表示在快照中的字符位置。 位置被保证都介于零和快照的长度。 一个<xref:Microsoft.VisualStudio.Text.SnapshotSpan>表示在快照中的文本范围。 保证其末尾的位置都介于零和快照的长度。 <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>包含的一组<xref:Microsoft.VisualStudio.Text.SnapshotSpan>在同一快照中的对象。  
  
#### <a name="spans-and-normalizedspancollections"></a>范围和 NormalizedSpanCollections  
 一个<xref:Microsoft.VisualStudio.Text.Span>表示可应用于文本快照中的文本范围的间隔。 快照位置是从零开始，因此范围可以在包括零个任何位置处开始。 `End`跨度的属性是否等于之和其`Start`属性并将其`Length`属性。 一个`Span`不包括按索引的字符`End`属性。 例如，具有的起始范围 = 5 且长度 = 3 具有最终 = 8，它包括在位置 5、 6 和 7 个字符。 此跨度的表示法是 5..8）。  
  
 这两个范围相交如果它们具有任何共同的位置，其中包括的结束位置。 因此的交集 [3, 5) 和 [2, 7) 是 [3, 5) 和的交集 [3, 5) 和 [5, 7) 是 [5，5）。 (请注意，[5，5) 是空范围。)  
  
 如果它们具有共同的位置，但的结束位置除外，这两个范围重叠。 空范围永远不会与任何其他范围重叠，并且永远不为空的两个范围重叠。  
  
 一个<xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection>是一系列按顺序启动属性范围的跨度。 在列表中，将合并重叠或相邻的范围。 例如，对于指定的范围集 [5..9)，[0..1)，[3..6)，和 [9..10)，规范化的列表的范围是 [0..1)，[3..10)。  
  
#### <a name="itextedit-textversion-and-text-change-notifications"></a>ITextEdit、 TextVersion 和文本更改通知  
 可以使用更改的文本缓冲区内容<xref:Microsoft.VisualStudio.Text.ITextEdit>对象。 创建此类对象 (通过使用之一`CreateEdit()`方法的<xref:Microsoft.VisualStudio.Text.ITextBuffer>) 启动包含的文本编辑的文本事务。 每次编辑是文本的某些范围的字符串缓冲区中的替代。 坐标和每次编辑内容相对于来表示缓冲区的快照事务启动时。 <xref:Microsoft.VisualStudio.Text.ITextEdit>对象调整编辑影响的其他编辑操作在同一事务中的坐标。  
  
 例如，考虑包含此字符串的文本缓冲区：  
  
```  
abcdefghij  
```  
  
 应用事务，其中包含两个编辑、 替换在 span 的一个编辑 [2..4) 使用的字符`X`，并替换在跨度第二个编辑 [6..9) 使用的字符`Y`。 结果是此缓冲区：  
  
```  
abXefYj  
```  
  
 第一次编辑应用之前，第二个编辑的坐标都计算方面的事务的开始处的缓冲区的内容。  
  
 对缓冲区更改才能生效时<xref:Microsoft.VisualStudio.Text.ITextEdit>对象提交通过调用其`Apply()`方法。 如果没有至少一个非空编辑，一个新<xref:Microsoft.VisualStudio.Text.ITextVersion>创建一个新<xref:Microsoft.VisualStudio.Text.ITextSnapshot>创建，且一个`Changed`引发事件。 每个文本版本都有不同文本快照。 文本快照后编辑事务，表示文本缓冲区的完成状态，但是文本版本描述仅从一个快照更改到下一步。 一般情况下，文本快照是用来使用一次，则丢弃，而文本版本段时间必须仍处于活动状态。  
  
 文本版本包含<xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection>。 此集合描述所做的更改，应用于快照时，将生成后续快照。 每个<xref:Microsoft.VisualStudio.Text.ITextChange>集合中包含的更改，在替换的字符串，并替换字符串的字符位置。 在替换的字符串为空基本的插入操作，并替换字符串是为基本删除空。 规范化的集合始终是`null`文本缓冲区的最新版本。  
  
 只有一个<xref:Microsoft.VisualStudio.Text.ITextEdit>可以实例化对象的文本缓冲区在任何时间，并必须拥有文本缓冲区 （如果已声明所有权） 的线程上执行所有文本编辑。 可以通过调用放弃文本编辑其`Cancel`方法或其`Dispose`方法。  
  
 <xref:Microsoft.VisualStudio.Text.ITextBuffer> 此外提供了`Insert()`， `Delete()`，并`Replace()`上找到类似的方法<xref:Microsoft.VisualStudio.Text.ITextEdit>接口。 这些调用不会有相同的效果与创建<xref:Microsoft.VisualStudio.Text.ITextEdit>对象，进行类似的调用，并应用编辑。  
  
#### <a name="tracking-points-and-tracking-spans"></a>跟踪点和跟踪范围  
 <xref:Microsoft.VisualStudio.Text.ITrackingPoint>表示文本缓冲区中的字符位置。 如果缓冲区编辑会导致要移动的字符的位置的方式，跟踪点将与之移动。 例如，如果跟踪点是指在缓冲区中，位置 10 和缓冲区开头位置插入五个字符，跟踪点然后指位置 15。 如果完成插入操作发生在精确地表示的跟踪点的位置，其行为由其<xref:Microsoft.VisualStudio.Text.PointTrackingMode>，这可以是`Positive`或`Negative`。 如果跟踪模式为正，跟踪点是指现插入; 结束时的相同字符如果跟踪模式为负，跟踪点是指位于原始位置的第一个插入字符。 如果删除由跟踪点的位置处的字符，则跟踪点将转移到已删除的范围的第一个字符。 例如，如果跟踪点指的是 5，位置处的字符，并且会删除在位置 3 到 6 个字符，跟踪点是指位置 3 处的字符。  
  
 <xref:Microsoft.VisualStudio.Text.ITrackingSpan>表示一系列字符而不是只需一个位置。 其行为由其<xref:Microsoft.VisualStudio.Text.SpanTrackingMode>。 如果范围跟踪模式，则<xref:Microsoft.VisualStudio.Text.SpanTrackingMode>，跟踪范围增长 s p a n 跟踪模式是将文本插入到其边缘; <xref:Microsoft.VisualStudio.Text.SpanTrackingMode>，跟踪范围未包含在其边缘处插入的文本。 但是，如果范围跟踪模式，则<xref:Microsoft.VisualStudio.Text.SpanTrackingMode>，完成插入操作将当前位置推送的开头，并且如果 s p a n 跟踪模式<xref:Microsoft.VisualStudio.Text.SpanTrackingMode>，完成插入操作将推送到结束当前的位置。  
  
 你可以获取文本缓冲区到其所属的任何快照的跟踪点的位置或跟踪范围的跨度。 跟踪点和跟踪范围可以安全地引用从任意线程。  
  
#### <a name="content-types"></a>内容类型  
 内容类型是内容的用于定义不同类型的机制。 内容类型可以是文件类型，例如"text"、"代码"或"binary"或"xml"、"vb"或"c#"等技术类型。 例如，单词"using"是关键字在 C# 和 Visual Basic 中，但不是在其他编程语言。 因此，此关键字的定义会限制为"c#"和"vb"内容类型。  
  
 内容类型用作筛选器修饰和编辑器的其他元素。 每个内容类型; 定义多个编辑器功能和扩展点例如，文本着色是不同的纯文本文件、 XML 文件和 Visual Basic 源代码文件。 创建，并且可以更改文本缓冲区的内容类型时，文本缓冲区通常会被分配的内容类型。  
  
 内容类型可以多-从其他内容类型继承。 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> ，可以指定多个基类型为给定的内容类型的父级。  
  
 开发人员可以定义自己的内容类型和使用注册<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>。 可通过使用相对于特定内容类型定义多个编辑器功能<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>。 例如，编辑器边距、 在修饰和鼠标处理程序可以定义，以便它们仅适用于显示特定内容类型的编辑器。  
  
### <a name="textview"></a> 文本视图  
 模型视图控制器 (MVC) 模式的视图部分定义的视图，如滚动条，并将插入符号的图形元素格式设置在文本视图。 在 Visual Studio 编辑器中的所有表示元素都基于 WPF。  
  
#### <a name="text-views"></a>文本视图  
 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>接口是独立于平台的表示形式的文本视图。 它主要用于文本文档显示在窗口中，但它还可用于其他目的，例如，在工具提示。  
  
 文本视图引用了不同类型的文本缓冲区。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A>属性是指<xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel>指向这些三个不同的文本缓冲区对象： 数据缓冲区是顶级数据级缓冲区中的编辑会发生，并且 visual 缓冲区，而这是缓冲区的编辑缓冲区文本视图中显示。  
  
 文本的格式根据附加到基础的文本缓冲区中，分类器，并且通过使用修饰提供程序附加到文本视图本身的修饰。  
  
#### <a name="the-text-view-coordinate-system"></a>文本视图坐标系统  
 文本视图坐标系统指定文本视图中的位置。 在此坐标系统中，x 值 0.0 对应于要显示的文本的左边缘和 y 值 0.0 对应于要显示的文本的上边缘。提高了从左到右的 x 坐标和 y 坐标会增加从上到下。  
  
 视区 （在文本窗口中可见的文本的部分） 不能是相同的方式水平滚动如垂直滚动。 通过更改其左边缘坐标，以便移动方面的绘图图面的水平滚动一个视区。 但是，视区可以滚动垂直只能通过更改呈现的文本，这会导致<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>事件被引发。  
  
 坐标系统中的距离对应于逻辑像素为单位。 如果不缩放转换的情况下显示的文本呈现图面，则文本呈现坐标系统中的一个单元对应于在显示屏上的一个像素。  
  
#### <a name="margins"></a>边距  
 <xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin>接口表示边距，并启用控件的边距和其大小的可见性。 有四个预定义的边距，后者并且名为"Top"、"左"、"Right""底部"并且附加到顶部、 底部、 左侧或视图的右边缘。 这些边距是可以在其中放置其他边距重叠的容器。 该接口定义返回边距的大小和边距的可见性的方法。 边距是提供其他信息附加到在文本视图的可视元素。 例如，行号边距显示文本视图的行号。 图标边距显示 UI 元素。  
  
 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider>接口处理创建和放置的边距。 可以相对于其他边距重叠排序边距。 优先级较高的边距中位于更靠近文本视图。 例如，如果有两个左右的边距、 边距 A 和 B、 边距和边距 B 具有比边距的较低优先级，边距 B 显示左侧边距 a。  
  
#### <a name="the-text-view-host"></a>文本视图主机  
 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>接口包含在文本视图和伴随的视图，例如，滚动条任何的装饰。 文本视图主机还包含附加到视图的边框的边距。  
  
#### <a name="formatted-text"></a>带格式的文本  
 在文本视图中显示的文本组成<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>对象。 每个文本视图行对应于一行文本视图中的文本。 基础文本缓冲区中的较长行可部分被遮盖 （如果未启用自动换行） 或已被分成多个文本视图行。 <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>接口包含方法和属性映射坐标之间的字符，然后可能与行相关联的修饰。  
  
 <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> 通过使用创建对象<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>接口。 如果你只想了解当前视图中显示的文本，可以忽略格式设置的源。 如果您感兴趣的不是文本格式显示在视图 （例如，若要支持富文本剪切并粘贴），则可以使用<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>来设置文本格式的文本缓冲区中。  
  
 文本视图格式之一<xref:Microsoft.VisualStudio.Text.ITextSnapshotLine>一次。  
  
## <a name="editor-features"></a>编辑器功能  
 编辑器的功能设计，以便独立于其实现的功能的定义。 编辑器包括以下功能：  
  
- 标记和分类器  
  
- 修饰  
  
- 投影  
  
- 大纲显示  
  
- 鼠标和键绑定  
  
- 操作和基元  
  
- IntelliSense  
  
### <a name="tagsandclassifiers"></a> 标记和分类器  
 标记是与文本范围的相关联的标记。 他们可以看到不同的方式，例如，通过使用文本着色、 下划线、 图形或弹出窗口。 分类器是标记的一种类型。  
  
 其他类型的标记都<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>突出显示文本，<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>用于大纲显示，和<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>的编译错误。  
  
#### <a name="classification-types"></a>分类类型  
 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>接口表示等价类，这是一个抽象的文本类别。 分类类型可以多-从其他分类类型继承。 例如，编程语言分类可能包括"关键字"、"注释"和"标识符"，它们都继承自"代码"。 自然语言分类类型可能包括"名词"、"谓词"和"修饰"的它们都继承自"自然语言"。  
  
#### <a name="classifications"></a>分类  
 分类通常是文本的跨度内的特定分类类型的实例。 一个<xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan>用于表示一个分类。 可以将分类跨度视为涵盖特定范围的文本，并告知系统，此范围的文本属于特定分类类型的标签。  
  
#### <a name="classifiers"></a>分类器  
 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier>是文本分解为一组分类的一种机制。 必须为特定的内容类型定义，为特定的文本缓冲区实例化分类器。 客户端必须实现<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>参与文本分类。  
  
#### <a name="classifier-aggregators"></a>分类器聚合器  
 分类器聚合器是一种机制，将一个文本缓冲区的所有分类器组合到一组分类。 例如，C# 分类器和一个英语语言的分类器可创建分类通过 C# 文件中的注释。 请考虑此注释：  
  
```  
// This method produces a classifier  
```  
  
 C# 分类器可能会标记为一个注释，整个范围并将英语语言的分类器可能会对其分类"生成"作为"谓词"和"method"作为"名词"。 聚合器生成一组非重叠的分类，并集的类型取决于发布的所有内容。  
  
 分类器聚合器也是一个分类器，因为它将文本分解为一组分类。 有没有重叠的分类和分类进行排序，还可以确保分类器聚合器。 单个分类器是按任意顺序返回任何一组分类，并以任何方式重叠。  
  
#### <a name="classification-formatting-and-text-coloring"></a>分类格式设置和文本着色  
 文本格式设置是基于文本分类特征的一个示例。 文本视图层使用它来确定应用程序中的中文本的显示。 文本格式设置区域是依赖于 WPF 中，但不是分类的逻辑定义。  
  
 分类格式是一组的格式设置为特定分类类型的属性。 这些格式继承分类类型的父级的格式。  
  
 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>是从分类类型的一系列文本格式设置属性的映射。 在编辑器中的格式映射的实现可处理分类格式的所有导出。  
  
### <a name="adornments"></a> 修饰  
 修饰是与的字体和颜色的文本视图中的字符不直接相关的图形效果。 例如，用于标记在许多编程语言的非编译代码的红色波浪线下划线是嵌入的修饰，而工具提示弹出窗口修饰。 修饰派生自<xref:System.Windows.UIElement>并实现<xref:Microsoft.VisualStudio.Text.Tagging.ITag>。 两种特殊类型的修饰标记<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>，为占用相同的空间，以在视图中，文本的修饰和<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>，为波浪线下划线。  
  
 嵌入的修饰是构成格式化的文本视图的一部分的图形。 在不同的 Z 顺序层，它们的组织方式。 有三个内置层，按如下所示： 文本、 插入符号和所选内容。 但是，开发人员可以定义多个层，并将其放在相对于另一个的顺序。 三种类型的嵌入修饰是相对于文本的修饰 （其中移动时移动文本，并删除文本时删除）、 相对于视图的修饰 （它们具有与非文本视图部分） 和所有者控制修饰 (开发人员必须管理它们的位置）。  
  
 弹出修饰是在文本视图，例如，工具提示上方的一个小窗口中显示的图形。  
  
### <a name="projection"></a> 投影  
 投影是一种构造一种不同的文本缓冲区的实际存储文本，但改为结合了其他文本缓冲区中的文本的方法。 例如，可以使用投影缓冲区，来连接其他两个缓冲区中的文本，并显示结果，如同它是一个缓冲区中或隐藏一个缓冲区中的文本部分。 投影缓冲区可以充当源缓冲区到另一个投影缓冲区。 可以构造一组缓冲区通过投影相关的顺序重新进行排列以多种不同方式的文本。 (此类集是也称为*缓冲区关系图*。)Visual Studio 文本大纲显示功能实现通过使用投影缓冲区来隐藏折叠的文本，并且 ASP.NET 页的 Visual Studio 编辑器使用投影来支持嵌入的 Visual Basic 和 C# 等语言。  
  
 <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>通过创建<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>。 投影缓冲区由的有序<xref:Microsoft.VisualStudio.Text.ITrackingSpan>对象被称为*源范围*。 这些范围的内容显示为一系列字符。 名为从中绘制源范围的文本缓冲区*源缓冲区*。 投影缓冲区的客户端就不必注意它不同于普通文本缓冲区。  
  
 投影缓冲区侦听对源缓冲区的文本更改事件。 在源中的文本范围发生了更改，投影缓冲区将更改的文本坐标映射到其自身的坐标，并引发适当的文本更改事件。 例如，考虑具有以下内容的源缓冲区 A 和 B:  
  
```  
A: ABCDE  
B: vwxyz  
```  
  
 如果投影缓冲区 P 格式从两个文本范围的所有缓冲区和另一个具有所有缓冲区 B，P 具有以下内容：  
  
```  
P: ABCDEvwxyz  
```  
  
 如果子字符串`xy`缓冲区 P 引发一个事件，指示已删除位置 7 和 8 个字符，然后从缓冲区 B，已删除。  
  
 此外可以直接编辑投影缓冲区。 它可传播到适当的源缓冲区的编辑。 例如，如果一个字符串插入到缓冲区 P 6 （"v"字符的原始位置） 的位置处，插入传播到缓冲区 B 中的位置 1。  
  
 没有上贡献投影缓冲区源范围的限制。 不能重叠的源跨度;投影缓冲区中的位置不能映射到在任何源缓冲区中的多个位置和源缓冲区中的位置不能映射到投影缓冲区中的多个位置。 源缓冲区关系中允许不使用任何迂回情况发生。  
  
 源组缓冲的投影缓冲区更改和源的一套跨更改时，将引发事件。  
  
 省略缓冲区是一种特殊的投影缓冲区。 主要使用大纲显示和操作的展开和折叠的文本块。 省略缓冲区取决于只是一个源缓冲区，并省略缓冲区中的范围必须排列在相同按照它们在源缓冲区进行排序。  
  
##### <a name="the-buffer-graph"></a>缓冲区关系图  
 <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>接口使跨投影缓冲区的图形映射。 所有文本缓冲区和投影缓冲区都收集在定向非循环图形，类似于由语言编译器生成的抽象语法树。 在关系图被定义的顶部缓冲区，可以是任何文本缓冲区。 从顶部到源缓冲区中的点缓冲区中的点或从顶部缓冲区的一系列源缓冲区中的范围中的范围，则可以将映射缓冲区关系图。 同样，它可以映射一个点或范围涵盖源缓冲区到顶部缓冲区中的点。 缓冲区关系图通过使用创建<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>。  
  
##### <a name="events-and-projection-buffers"></a>事件和投影缓冲区  
 修改投影缓冲区后，所做的修改将从投影缓冲区发送到依赖于它的缓冲区。 修改所有缓冲区后，会引发缓冲区更改事件，从最深的缓冲区。  
  
### <a name="outlining"></a> 大纲显示  
 大纲显示是文本的能够展开或折叠不同的文本视图中块。 大纲显示定义为一种类型的<xref:Microsoft.VisualStudio.Text.Tagging.ITag>中的相同方式定义修饰。 一个<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>是定义可以展开或折叠的文本区域的标记。 若要使用大纲显示，必须导入<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>若要获取<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>。 大纲显示管理器枚举，折叠，且扩展，不同的块，该值表示为<xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible>对象，并相应地引发事件。  
  
### <a name="mousebindings"></a> 鼠标绑定  
 鼠标绑定链接鼠标移动到不同的命令。 通过使用定义鼠标绑定<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider>，并通过使用定义键绑定<xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider>。 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>自动实例化的所有绑定，并将其连接到视图中的鼠标事件。  
  
 <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor>接口包含不同的鼠标事件的预处理和后处理事件处理程序。 为其中一个事件句柄，您可以重写中的方法的一些<xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase>。  
  
### <a name="editoroperations"></a> 编辑器操作  
 可以使用编辑器操作来自动执行与编辑器中的，用于编写脚本或其他目的进行交互。 您可以导入<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>上访问操作到给定<xref:Microsoft.VisualStudio.Text.Editor.ITextView>。 然后可以使用这些对象以修改所选内容、 滚动视图，或将插入符号移动到视图的不同部分。  
  
### <a name="intellisense"></a> IntelliSense  
 IntelliSense 支持语句完成、 签名帮助 （也称为参数信息）、 快速信息和灯泡。  
  
 语句补全将提供方法名称、 XML 元素和其他编码或标记元素的潜在完成弹出的列表。 一般情况下，用户手势调用完成会话。 潜在的完成列表将显示会话和用户可以选择一个或消除列表。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>负责创建并触发<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>计算<xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet>会话完成项。  
  
## <a name="see-also"></a>请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)   
 [编辑器导入](../extensibility/editor-imports.md)
