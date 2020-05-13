---
title: 演练：突出显示文本 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - highlight text
ms.assetid: 64b772ad-4392-42e9-a237-5137f0384bf0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c35b1a032993a6c183191aafff77d8adeba4a3ef
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697393"
---
# <a name="walkthrough-highlight-text"></a>演练：突出显示文本
您可以通过创建托管扩展框架 （MEF） 组件部件向编辑器添加不同的视觉效果。 本演练演示如何突出显示文本文件中当前单词的每个匹配项。 如果一个单词在文本文件中发生不止一次，并且将 caret 定位在一个匹配项中，则每个匹配项都会突出显示。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`HighlightWordTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="define-a-textmarkertag"></a>定义文本标记
 突出显示文本的第一步是子类<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>并定义其外观。

### <a name="to-define-a-textmarkertag-and-a-markerformatdefinition"></a>定义文本标记和标记格式定义

1. 添加类文件并将其命名为 **"高光WordTag"。**

2. 添加以下引用：

    1. 微软.VisualStudio.核心实用程序

    2. 微软.VisualStudio.文本.数据

    3. 微软.VisualStudio.文本.逻辑

    4. 微软.VisualStudio.文本.UI

    5. 微软.VisualStudio.文本.UI.Wpf

    6. System.ComponentModel.Composition

    7. 演示文稿.核心

    8. 演示.框架

3. 导入以下命名空间。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using System.Threading;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Text.Tagging;
    using Microsoft.VisualStudio.Utilities;
    using System.Windows.Media;
    ```

4. 创建继承<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>并命名它的`HighlightWordTag`类。

    ```csharp
    internal class HighlightWordTag : TextMarkerTag
    {

    }
    ```

5. 创建从<xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>继承的第二个类并命名它`HighlightWordFormatDefinition`。 为了对标记使用此格式定义，必须使用以下属性导出它：

    - <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：标记用它来引用此格式

    - <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>：这将导致格式显示在 UI 中

    ```csharp

    [Export(typeof(EditorFormatDefinition))]
    [Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
    [UserVisible(true)]
    internal class HighlightWordFormatDefinition : MarkerFormatDefinition
    {

    }
    ```

6. 在高光字格式定义的构造函数中，定义其显示名称和外观。 "背景"属性定义填充颜色，而"前景"属性定义边框颜色。

    ```csharp
    public HighlightWordFormatDefinition()
    {
                this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
    ```

7. 在高光WordTag的构造函数中，以您创建的格式定义的名称传递。

    ```
    public HighlightWordTag() : base("MarkerFormatDefinition/HighlightWordFormatDefinition") { }
    ```

## <a name="implement-an-itagger"></a>实施 ITagger
 下一步是实现接口<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>。 此接口为给定的文本缓冲区分配提供文本突出显示和其他视觉效果的标记。

### <a name="to-implement-a-tagger"></a>实现标记

1. 创建实现类型的<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>`HighlightWordTag`类 ，并命名它`HighlightWordTagger`。

    ```csharp
    internal class HighlightWordTagger : ITagger<HighlightWordTag>
    {

    }
    ```

2. 将以下私有字段和属性添加到类：

    - 对应于<xref:Microsoft.VisualStudio.Text.Editor.ITextView>当前文本视图的 。

    - 对应于<xref:Microsoft.VisualStudio.Text.ITextBuffer>文本视图的基础的文本缓冲区。

    - 用于<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>查找文本的 。

    - 具有<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>在文本范围内导航的方法。

    - 包含<xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>要突出显示的单词集。

    - 对应于<xref:Microsoft.VisualStudio.Text.SnapshotSpan>当前单词的 。

    - 对应于<xref:Microsoft.VisualStudio.Text.SnapshotPoint>caret 的当前位置。

    - 锁定对象。

    ```csharp
    ITextView View { get; set; }
    ITextBuffer SourceBuffer { get; set; }
    ITextSearchService TextSearchService { get; set; }
    ITextStructureNavigator TextStructureNavigator { get; set; }
    NormalizedSnapshotSpanCollection WordSpans { get; set; }
    SnapshotSpan? CurrentWord { get; set; }
    SnapshotPoint RequestedPoint { get; set; }
    object updateLock = new object();

    ```

3. 添加一个构造函数，用于初始化前面列出的属性，并<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>添加<xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged>和事件处理程序。

    ```csharp
    public HighlightWordTagger(ITextView view, ITextBuffer sourceBuffer, ITextSearchService textSearchService,
    ITextStructureNavigator textStructureNavigator)
    {
        this.View = view;
        this.SourceBuffer = sourceBuffer;
        this.TextSearchService = textSearchService;
        this.TextStructureNavigator = textStructureNavigator;
        this.WordSpans = new NormalizedSnapshotSpanCollection();
        this.CurrentWord = null;
        this.View.Caret.PositionChanged += CaretPositionChanged;
        this.View.LayoutChanged += ViewLayoutChanged;
    }

    ```

4. 事件处理程序都调用 方法`UpdateAtCaretPosition`。

    ```csharp
    void ViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        // If a new snapshot wasn't generated, then skip this layout 
        if (e.NewSnapshot != e.OldSnapshot)
        {
            UpdateAtCaretPosition(View.Caret.Position);
        }
    }

    void CaretPositionChanged(object sender, CaretPositionChangedEventArgs e)
    {
        UpdateAtCaretPosition(e.NewPosition);
    }
    ```

5. 还必须添加更新方法调用`TagsChanged`的事件。

     [!code-csharp[VSSDKHighlightWordTest#10](../extensibility/codesnippet/CSharp/walkthrough-highlighting-text_1.cs)]
     [!code-vb[VSSDKHighlightWordTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-highlighting-text_1.vb)]

6. 该方法`UpdateAtCaretPosition()`查找文本缓冲区中与光标定位的单词相同的每个单词，并构造对应于该单词出现<xref:Microsoft.VisualStudio.Text.SnapshotSpan>的对象列表。 然后调用`SynchronousUpdate`，引发事件`TagsChanged`。

    ```csharp
    void UpdateAtCaretPosition(CaretPosition caretPosition)
    {
        SnapshotPoint? point = caretPosition.Point.GetPoint(SourceBuffer, caretPosition.Affinity);

        if (!point.HasValue)
            return;

        // If the new caret position is still within the current word (and on the same snapshot), we don't need to check it 
        if (CurrentWord.HasValue
            && CurrentWord.Value.Snapshot == View.TextSnapshot
            && point.Value >= CurrentWord.Value.Start
            && point.Value <= CurrentWord.Value.End)
        {
            return;
        }

        RequestedPoint = point.Value;
        UpdateWordAdornments();
    }

    void UpdateWordAdornments()
    {
        SnapshotPoint currentRequest = RequestedPoint;
        List<SnapshotSpan> wordSpans = new List<SnapshotSpan>();
        //Find all words in the buffer like the one the caret is on
        TextExtent word = TextStructureNavigator.GetExtentOfWord(currentRequest);
        bool foundWord = true;
        //If we've selected something not worth highlighting, we might have missed a "word" by a little bit
        if (!WordExtentIsValid(currentRequest, word))
        {
            //Before we retry, make sure it is worthwhile 
            if (word.Span.Start != currentRequest
                 || currentRequest == currentRequest.GetContainingLine().Start
                 || char.IsWhiteSpace((currentRequest - 1).GetChar()))
            {
                foundWord = false;
            }
            else
            {
                // Try again, one character previous.  
                //If the caret is at the end of a word, pick up the word.
                word = TextStructureNavigator.GetExtentOfWord(currentRequest - 1);

                //If the word still isn't valid, we're done 
                if (!WordExtentIsValid(currentRequest, word))
                    foundWord = false;
            }
        }

        if (!foundWord)
        {
            //If we couldn't find a word, clear out the existing markers
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(), null);
            return;
        }

        SnapshotSpan currentWord = word.Span;
        //If this is the current word, and the caret moved within a word, we're done. 
        if (CurrentWord.HasValue && currentWord == CurrentWord)
            return;

        //Find the new spans
        FindData findData = new FindData(currentWord.GetText(), currentWord.Snapshot);
        findData.FindOptions = FindOptions.WholeWord | FindOptions.MatchCase;

        wordSpans.AddRange(TextSearchService.FindAll(findData));

        //If another change hasn't happened, do a real update 
        if (currentRequest == RequestedPoint)
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(wordSpans), currentWord);
    }
    static bool WordExtentIsValid(SnapshotPoint currentRequest, TextExtent word)
    {
        return word.IsSignificant
            && currentRequest.Snapshot.GetText(word.Span).Any(c => char.IsLetter(c));
    }

    ```

7. `SynchronousUpdate`对`WordSpans`和`CurrentWord`属性执行同步更新，并引发事件`TagsChanged`。

    ```csharp
    void SynchronousUpdate(SnapshotPoint currentRequest, NormalizedSnapshotSpanCollection newSpans, SnapshotSpan? newCurrentWord)
    {
        lock (updateLock)
        {
            if (currentRequest != RequestedPoint)
                return;

            WordSpans = newSpans;
            CurrentWord = newCurrentWord;

            var tempEvent = TagsChanged;
            if (tempEvent != null)
                tempEvent(this, new SnapshotSpanEventArgs(new SnapshotSpan(SourceBuffer.CurrentSnapshot, 0, SourceBuffer.CurrentSnapshot.Length)));
        }
    }
    ```

8. 您必须实现该方法<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>。 此方法获取<xref:Microsoft.VisualStudio.Text.SnapshotSpan>对象的集合，并返回标记范围的枚举。

     在 C# 中，将此方法实现为屈服迭代器，该迭代器支持标记的延迟计算（即仅在访问单个项时评估集）。 在"可视基本"中，将标记添加到列表中并返回列表。

     在这里，该方法返回具有<xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601>"蓝色"<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>的对象，该对象提供蓝色背景。

    ```csharp
    public IEnumerable<ITagSpan<HighlightWordTag>> GetTags(NormalizedSnapshotSpanCollection spans)
    {
        if (CurrentWord == null)
            yield break;

        // Hold on to a "snapshot" of the word spans and current word, so that we maintain the same
        // collection throughout
        SnapshotSpan currentWord = CurrentWord.Value;
        NormalizedSnapshotSpanCollection wordSpans = WordSpans;

        if (spans.Count == 0 || wordSpans.Count == 0)
            yield break;

        // If the requested snapshot isn't the same as the one our words are on, translate our spans to the expected snapshot 
        if (spans[0].Snapshot != wordSpans[0].Snapshot)
        {
            wordSpans = new NormalizedSnapshotSpanCollection(
                wordSpans.Select(span => span.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive)));

            currentWord = currentWord.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive);
        }

        // First, yield back the word the cursor is under (if it overlaps) 
        // Note that we'll yield back the same word again in the wordspans collection; 
        // the duplication here is expected. 
        if (spans.OverlapsWith(new NormalizedSnapshotSpanCollection(currentWord)))
            yield return new TagSpan<HighlightWordTag>(currentWord, new HighlightWordTag());

        // Second, yield all the other words in the file 
        foreach (SnapshotSpan span in NormalizedSnapshotSpanCollection.Overlap(spans, wordSpans))
        {
            yield return new TagSpan<HighlightWordTag>(span, new HighlightWordTag());
        }
    }
    ```

## <a name="create-a-tagger-provider"></a>创建标记提供程序
 要创建标记器，必须实现 。 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> 此类是 MEF 组件部分，因此必须设置正确的属性，以便识别此扩展。

> [!NOTE]
> 有关 MEF 的详细信息，请参阅[托管扩展性框架 （MEF）。](/dotnet/framework/mef/index)

### <a name="to-create-a-tagger-provider"></a>创建标记提供程序

1. 创建名为 的`HighlightWordTaggerProvider`类，<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>实现 ，并导出它<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>与 的 "文本<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>"<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>和 a

    ```csharp
    [Export(typeof(IViewTaggerProvider))]
    [ContentType("text")]
    [TagType(typeof(TextMarkerTag))]
    internal class HighlightWordTaggerProvider : IViewTaggerProvider
    { }
    ```

2. 您必须导入两个编辑器服务，和<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService><xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，以实例化标记。

    ```csharp
    [Import]
    internal ITextSearchService TextSearchService { get; set; }

    [Import]
    internal ITextStructureNavigatorSelectorService TextStructureNavigatorSelector { get; set; }

    ```

3. 实现方法<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>以返回 的`HighlightWordTagger`实例。

    ```csharp
    public ITagger<T> CreateTagger<T>(ITextView textView, ITextBuffer buffer) where T : ITag
    {
        //provide highlighting only on the top buffer 
        if (textView.TextBuffer != buffer)
            return null;

        ITextStructureNavigator textStructureNavigator =
            TextStructureNavigatorSelector.GetTextStructureNavigator(buffer);

        return new HighlightWordTagger(textView, buffer, TextSearchService, textStructureNavigator) as ITagger<T>;
    }
    ```

## <a name="build-and-test-the-code"></a>生成和测试代码
 要测试此代码，请构建高光WordTest解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-highlightwordtest-solution"></a>构建和测试高光字测试解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建文本文件并键入一些重复单词的文本，例如"你好你好"。

4. 将光标放置在"hello"的一个事件中。 每个事件都应以蓝色突出显示。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
