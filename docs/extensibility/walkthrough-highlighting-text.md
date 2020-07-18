---
title: 演练：突出显示文本 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - highlight text
ms.assetid: 64b772ad-4392-42e9-a237-5137f0384bf0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0331c0d240503dd88257269397e1afae80a17803
ms.sourcegitcommit: 0f30188f57d5ad2b0c8073eb51d37557c8f35a62
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418063"
---
# <a name="walkthrough-highlight-text"></a>演练：突出显示文本
您可以通过创建 Managed Extensibility Framework （MEF）组件部分向编辑器添加不同的视觉效果。 本演练演示如何突出显示文本文件中当前单词的每个匹配项。 如果某个单词在文本文件中出现多次，并且您将插入符号放置在一个匹配项中，则将突出显示每个匹配项。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 c # VSIX 项目。 （在 "**新建项目**" 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。）命名解决方案 `HighlightWordTest` 。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="define-a-textmarkertag"></a>定义 TextMarkerTag
 突出显示文本的第一步是为子类 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 并定义其外观。

### <a name="to-define-a-textmarkertag-and-a-markerformatdefinition"></a>定义 TextMarkerTag 和 MarkerFormatDefinition

1. 添加一个类文件并将其命名为**HighlightWordTag**。

2. 添加以下引用：

    1. VisualStudio. CoreUtility

    2. VisualStudio 数据

    3. VisualStudio。

    4. VisualStudio。

    5. VisualStudio （& e）

    6. System.ComponentModel.Composition

    7. Presentation Core

    8. Presentation Framework

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

4. 创建一个继承自的类 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 并将其命名为 `HighlightWordTag` 。

    ```csharp
    internal class HighlightWordTag : TextMarkerTag
    {

    }
    ```

5. 创建从继承的第二个类 <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> ，并为其命名 `HighlightWordFormatDefinition` 。 若要将此格式定义用于标记，必须使用以下属性导出它：

    - <xref:Microsoft.VisualStudio.Utilities.NameAttribute>：标记用于引用此格式

    - <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>：这将导致在 UI 中显示格式

    ```csharp

    [Export(typeof(EditorFormatDefinition))]
    [Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
    [UserVisible(true)]
    internal class HighlightWordFormatDefinition : MarkerFormatDefinition
    {

    }
    ```

6. 在 HighlightWordFormatDefinition 的构造函数中，定义其显示名称和外观。 背景属性定义填充颜色，而前景属性定义边框颜色。

    ```csharp
    public HighlightWordFormatDefinition()
    {
        this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
    ```

7. 在 HighlightWordTag 的构造函数中，传递所创建的格式定义的名称。

    ```
    public HighlightWordTag() : base("MarkerFormatDefinition/HighlightWordFormatDefinition") { }
    ```

## <a name="implement-an-itagger"></a>实现 ITagger
 下一步是实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 接口。 此接口将分配给给定文本缓冲区、提供文本突出显示的标记和其他视觉效果。

### <a name="to-implement-a-tagger"></a>实现标记

1. 创建一个 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 类型为的类 `HighlightWordTag` ，并为其命名 `HighlightWordTagger` 。

    ```csharp
    internal class HighlightWordTagger : ITagger<HighlightWordTag>
    {

    }
    ```

2. 将以下私有字段和属性添加到类：

    - <xref:Microsoft.VisualStudio.Text.Editor.ITextView>，它对应于当前文本视图。

    - <xref:Microsoft.VisualStudio.Text.ITextBuffer>，它对应于文本视图的基础文本缓冲区。

    - <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>用于查找文本的。

    - <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>，它具有在文本范围中导航的方法。

    - 一个 <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection> ，其中包含要突出显示的字词集。

    - <xref:Microsoft.VisualStudio.Text.SnapshotSpan>，它对应于当前单词。

    - <xref:Microsoft.VisualStudio.Text.SnapshotPoint>，它对应于插入符号的当前位置。

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

3. 添加一个构造函数，用于初始化前面列出的属性并添加 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> 和 <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> 事件处理程序。

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

4. 事件处理程序都调用 `UpdateAtCaretPosition` 方法。

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

5. 还必须添加 `TagsChanged` 由 update 方法调用的事件。

     [!code-csharp[VSSDKHighlightWordTest#10](../extensibility/codesnippet/CSharp/walkthrough-highlighting-text_1.cs)]
     [!code-vb[VSSDKHighlightWordTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-highlighting-text_1.vb)]

6. `UpdateAtCaretPosition()`方法查找文本缓冲区中与光标所在位置相同的每个单词，并构造 <xref:Microsoft.VisualStudio.Text.SnapshotSpan> 与出现单词匹配的对象的列表。 然后，它调用 `SynchronousUpdate` 引发事件的 `TagsChanged` 。

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

7. 对 `SynchronousUpdate` 和属性执行同步更新 `WordSpans` `CurrentWord` ，并引发 `TagsChanged` 事件。

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

8. 必须实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> 方法。 此方法获取对象的集合 <xref:Microsoft.VisualStudio.Text.SnapshotSpan> ，并返回标记跨度的枚举。

     在 c # 中，将此方法实现为 yield 迭代器，该迭代器对标记启用延迟计算（即，仅在访问个别项时对集进行计算）。 在 Visual Basic 中，将标记添加到列表并返回列表。

     此方法返回一个 <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> 具有 "blue" 的对象 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ，该对象提供蓝色背景。

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

## <a name="create-a-tagger-provider"></a>创建标记器提供程序
 若要创建标记，必须实现 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> 。 此类是一个 MEF 组件部件，因此必须设置正确的属性，以便识别此扩展。

> [!NOTE]
> 有关 MEF 的详细信息，请参阅[Managed Extensibility Framework （MEF）](/dotnet/framework/mef/index)。

### <a name="to-create-a-tagger-provider"></a>创建标记器提供程序

1. 创建一个名为的类，该类 `HighlightWordTaggerProvider` 实现 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> ，并将其导出为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" 和的 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。

    ```csharp
    [Export(typeof(IViewTaggerProvider))]
    [ContentType("text")]
    [TagType(typeof(TextMarkerTag))]
    internal class HighlightWordTaggerProvider : IViewTaggerProvider
    { }
    ```

2. 您必须导入两个编辑器服务， <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService> 以及 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 用于实例化标记的。

    ```csharp
    [Import]
    internal ITextSearchService TextSearchService { get; set; }

    [Import]
    internal ITextStructureNavigatorSelectorService TextStructureNavigatorSelector { get; set; }

    ```

3. 实现 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> 方法以返回的实例 `HighlightWordTagger` 。

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
 若要测试此代码，请生成 HighlightWordTest 解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-highlightwordtest-solution"></a>生成和测试 HighlightWordTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，在其中重复单词，例如 "hello hello hello"。

4. 将光标置于出现的 "hello" 之一中。 每个匹配项都应以蓝色突出显示。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
