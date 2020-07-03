---
title: 演练：显示灯泡建议 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 153eda065b9a6e845a39c35aaae34bbe1745f7a8
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904998"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>演练：显示灯泡建议
轻型电灯泡是 Visual Studio 编辑器中的图标，可展开以显示一组操作，例如对内置代码分析器或代码重构标识的问题的修补程序。

 在 Visual c # 和 Visual Basic 编辑器中，还可以使用 .NET Compiler Platform （"Roslyn"）来编写和打包自己的代码分析器，其中包含自动电灯泡显示的操作。 有关详情，请参阅：

- [如何：编写 c # 诊断和代码修补程序](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)

- [如何：编写 Visual Basic 诊断和代码修补程序](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix)

  其他语言（如 c + +）还为某些快速操作提供了轻电灯泡，例如，创建该函数的存根实现的建议。

  灯泡的外观如下所示。 在 Visual Basic 或 Visual c # 项目中，如果变量名称无效，则会出现红色波形曲线。 如果将鼠标悬停在无效的标识符上，则光标附近会出现一个灯泡。

  ![灯泡](../extensibility/media/lightbulb.png "灯泡")

  如果单击灯泡的下箭头，将显示一组建议的操作，以及所选操作的预览。 在这种情况下，它会在执行操作时显示对代码所做的更改。

  ![灯泡预览](../extensibility/media/lightbulbpreview.png "LightBulbPreview")

  可以使用轻型电灯泡来提供自己的建议操作。 例如，可以提供将左大括号移动到新行或将其移动到上一行末尾的操作。 下面的演练演示如何创建出现在当前单词上的灯泡，并提供两个建议的操作： "**转换为大写**" 和 "**转换为小写**"。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework （MEF）项目

1. 创建 c # VSIX 项目。 （在 "**新建项目**" 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。）命名解决方案 `LightBulbTest` 。

2. 将**编辑器分类器**项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 将以下引用添加到项目，并将 "**复制本地**" 设置为 `False` ：

     *Microsoft.VisualStudio.Language.Intellisense*

5. 添加新的类文件并将其命名为**LightBulbTest**。

6. 添加以下 using 指令：

    ```csharp
    using System;
    using System.Linq;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    using Microsoft.VisualStudio.Language.Intellisense;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Utilities;
    using System.ComponentModel.Composition;
    using System.Threading;

    ```

## <a name="implement-the-light-bulb-source-provider"></a>实现灯泡源提供程序

1. 在*LightBulbTest.cs*类文件中，删除 LightBulbTest 类。 添加一个名为**TestSuggestedActionsSourceProvider**的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> 。 使用 "**测试建议的操作**" 和 "文本" 的名称导出它 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 。

    ```csharp
    [Export(typeof(ISuggestedActionsSourceProvider))]
    [Name("Test Suggested Actions")]
    [ContentType("text")]
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider
    ```

2. 在源提供程序类中，导入， <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 并将其添加为属性。

    ```csharp
    [Import(typeof(ITextStructureNavigatorSelectorService))]
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }
    ```

3. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A> 方法以返回 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> 对象。 下一节将讨论该源。

    ```csharp
    public ISuggestedActionsSource CreateSuggestedActionsSource(ITextView textView, ITextBuffer textBuffer)
    {
        if (textBuffer == null || textView == null)
        {
            return null;
        }
        return new TestSuggestedActionsSource(this, textView, textBuffer);
    }
    ```

## <a name="implement-the-isuggestedactionsource"></a>实现 ISuggestedActionSource
 建议的操作源负责收集一组建议的操作，并将其添加到正确的上下文中。 在这种情况下，上下文是当前词，建议的操作是**UpperCaseSuggestedAction**和**LowerCaseSuggestedAction**，如下一节中所述。

1. 添加一个实现的**TestSuggestedActionsSource**类 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> 。

    ```csharp
    internal class TestSuggestedActionsSource : ISuggestedActionsSource
    ```

2. 为建议的操作源提供程序、文本缓冲区和文本视图添加私有只读字段。

    ```csharp
    private readonly TestSuggestedActionsSourceProvider m_factory;
    private readonly ITextBuffer m_textBuffer;
    private readonly ITextView m_textView;
    ```

3. 添加用于设置私有字段的构造函数。

    ```csharp
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)
    {
        m_factory = testSuggestedActionsSourceProvider;
        m_textBuffer = textBuffer;
        m_textView = textView;
    }
    ```

4. 添加返回当前光标下的单词的私有方法。 以下方法将查看光标的当前位置，并向文本结构导航器询问单词范围。 如果光标位于某个单词上，则将 <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> 在 out 参数中返回; 否则，该 `out` 参数为 `null` ，并且该方法将返回 `false` 。

    ```csharp
    private bool TryGetWordUnderCaret(out TextExtent wordExtent)
    {
        ITextCaret caret = m_textView.Caret;
        SnapshotPoint point;

        if (caret.Position.BufferPosition > 0)
        {
            point = caret.Position.BufferPosition - 1;
        }
        else
        {
            wordExtent = default(TextExtent);
            return false;
        }

        ITextStructureNavigator navigator = m_factory.NavigatorService.GetTextStructureNavigator(m_textBuffer);

        wordExtent = navigator.GetExtentOfWord(point);
        return true;
    }
    ```

5. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> 方法。 编辑器调用此方法来确定是否显示灯泡。 例如，当光标从一行移到另一条时，或者当鼠标悬停在错误的曲线上时，通常会进行此调用。 在此方法运行时，它是异步的，以便允许其他 UI 操作执行。 在大多数情况下，此方法需要对当前行执行一些分析和分析操作，因此处理过程可能需要一些时间。

     在此实现中，它以异步方式获取， <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> 并确定范围是否重要，如中是否包含除空白以外的其他文本。

    ```csharp
    public Task<bool> HasSuggestedActionsAsync(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        return Task.Factory.StartNew(() =>
        {
            TextExtent extent;
            if (TryGetWordUnderCaret(out extent))
            {
                // don't display the action if the extent has whitespace
                return extent.IsSignificant;
              }
            return false;
        });
    }
    ```

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A> 方法，该方法返回 <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> 包含不同对象的对象的数组 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> 。 此方法在展开灯泡时进行调用。

    > [!WARNING]
    > 你应确保和的实现 `HasSuggestedActionsAsync()` `GetSuggestedActions()` 一致; 即，如果 `HasSuggestedActionsAsync()` 返回 `true` ，则 `GetSuggestedActions()` 应具有要显示的一些操作。 在许多情况下， `HasSuggestedActionsAsync()` 只会在之前调用 `GetSuggestedActions()` ，但这并不总是如此。 例如，如果用户通过按（**CTRL +** .）调用灯泡操作， `GetSuggestedActions()` 则只调用。

    ```csharp
    public IEnumerable<SuggestedActionSet> GetSuggestedActions(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        TextExtent extent;
        if (TryGetWordUnderCaret(out extent) && extent.IsSignificant)
        {
            ITrackingSpan trackingSpan = range.Snapshot.CreateTrackingSpan(extent.Span, SpanTrackingMode.EdgeInclusive);
            var upperAction = new UpperCaseSuggestedAction(trackingSpan);
            var lowerAction = new LowerCaseSuggestedAction(trackingSpan);
            return new SuggestedActionSet[] { new SuggestedActionSet(new ISuggestedAction[] { upperAction, lowerAction }) };
        }
        return Enumerable.Empty<SuggestedActionSet>();
    }
    ```

7. 定义 `SuggestedActionsChanged` 事件。

    ```csharp
    public event EventHandler<EventArgs> SuggestedActionsChanged;
    ```

8. 若要完成实现，请添加 `Dispose()` 和方法的实现 `TryGetTelemetryId()` 。 你不想要执行遥测操作，因此只需返回 `false` 并将 GUID 设置为 `Empty` 。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample provider and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

## <a name="implement-light-bulb-actions"></a>实现灯泡操作

1. 在项目中，添加对*Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll*的引用并将 "**复制本地**" 设置为 `False` 。

2. 创建两个类，第一个名为 `UpperCaseSuggestedAction` ，第二个名为 `LowerCaseSuggestedAction`。 两个类都实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>。

    ```csharp
    internal class UpperCaseSuggestedAction : ISuggestedAction
    internal class LowerCaseSuggestedAction : ISuggestedAction
    ```

     这两个类相似，只不过其中一个调用 <xref:System.String.ToUpper%2A>，另一个调用 <xref:System.String.ToLower%2A>。 以下步骤仅说明大写操作类，但你必须实现这两个类。 将实现大写操作的步骤用作实现小写操作的模式。

3. 为这些类添加以下 using 指令：

    ```csharp
    using Microsoft.VisualStudio.Imaging.Interop;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Documents;
    using System.Windows.Media;

    ```

4. 声明一组私有字段。

    ```csharp
    private ITrackingSpan m_span;
    private string m_upper;
    private string m_display;
    private ITextSnapshot m_snapshot;
    ```

5. 添加设置该字段的构造函数。

    ```csharp
    public UpperCaseSuggestedAction(ITrackingSpan span)
    {
        m_span = span;
        m_snapshot = span.TextBuffer.CurrentSnapshot;
        m_upper = span.GetText(m_snapshot).ToUpper();
        m_display = string.Format("Convert '{0}' to upper case", span.GetText(m_snapshot));
    }
    ```

6. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A> 方法，使其显示操作预览。

    ```csharp
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)
    {
        var textBlock = new TextBlock();
        textBlock.Padding = new Thickness(5);
        textBlock.Inlines.Add(new Run() { Text = m_upper });
        return Task.FromResult<object>(textBlock);
    }
    ```

7. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A> 方法，使其返回空 <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> 枚举。

    ```csharp
    public Task<IEnumerable<SuggestedActionSet>> GetActionSetsAsync(CancellationToken cancellationToken)
    {
        return Task.FromResult<IEnumerable<SuggestedActionSet>>(null);
    }
    ```

8. 如下所示实现属性。

    ```csharp
    public bool HasActionSets
    {
        get { return false; }
    }
    public string DisplayText
    {
        get { return m_display; }
    }
    public ImageMoniker IconMoniker
    {
       get { return default(ImageMoniker); }
    }
    public string IconAutomationText
    {
        get
        {
            return null;
        }
    }
    public string InputGestureText
    {
        get
        {
            return null;
        }
    }
    public bool HasPreview
    {
        get { return true; }
    }
    ```

9. 通过将范围中的文本替换为其大写形式来实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.Invoke%2A> 方法。

    ```csharp
    public void Invoke(CancellationToken cancellationToken)
    {
        m_span.TextBuffer.Replace(m_span.GetSpan(m_snapshot), m_upper);
    }
    ```

    > [!WARNING]
    > 灯泡操作**调用**方法不应显示 UI。 如果你的操作确实会引入新的 UI （例如，预览或选择对话框），请不要直接从**invoke**方法中显示 ui，而是计划在从**invoke**返回后显示 ui。

10. 若要完成实现，请添加 `Dispose()` 和 `TryGetTelemetryId()` 方法。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample action and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

11. 不要忘记执行相同的操作，将 `LowerCaseSuggestedAction` 显示文本更改为 "转换为 {0} 小写"，并调用 <xref:System.String.ToUpper%2A> <xref:System.String.ToLower%2A> 。

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 LightBulbTest 解决方案并在实验实例中运行它。

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本。 文本的左侧应显示一个灯泡。

     ![测试灯泡](../extensibility/media/testlightbulb.png "TestLIghtBulb")

4. 点亮。 应会看到向下箭头。

5. 单击灯泡时，应显示两个建议的操作，以及所选操作的预览。

     ![测试灯泡，已展开](../extensibility/media/testlightbulbexpanded.gif "TestLIghtBulbExpanded")

6. 如果单击第一个操作，则当前单词中的所有文本都将转换为大写形式。 如果单击第二个操作，则所有文本都应转换为小写。
