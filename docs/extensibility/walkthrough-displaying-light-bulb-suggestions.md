---
title: 演练：显示灯泡建议 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 09773e2be81ce51971709db590a07ca9960104fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697475"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>演练：显示灯泡建议
灯泡是 Visual Studio 编辑器中的图标，可展开以显示一组操作，例如，修复内置代码分析器或代码重构识别的问题。

 在 Visual C++ 和 Visual Basic 编辑器中，您还可以使用 .NET 编译器平台（"Roslyn"）编写和打包您自己的代码分析器，并自动显示灯泡。 有关详细信息，请参见:

- [如何：编写 C# 诊断和代码修复](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)

- [如何：编写可视化基本诊断和代码修复](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix)

  其他语言（如C++）也为一些快速操作提供灯泡，例如，建议创建该函数的存根实现。

  灯泡是什么样子的。 在可视化基本或视觉 C++ 项目中，红色波浪形在变量名称下显示无效。 如果鼠标悬停在无效标识符上，光标附近将显示一个灯泡。

  ![灯泡](../extensibility/media/lightbulb.png "灯泡")

  如果按灯泡单击向下箭头，将显示一组建议的操作以及所选操作的预览。 在这种情况下，它会显示执行操作时对代码所做的更改。

  ![灯泡预览](../extensibility/media/lightbulbpreview.png "灯泡预览")

  您可以使用灯泡提供您自己的建议操作。 例如，可以提供操作，将左大括号移动到新行或将它们移动到上一行的末尾。 下面的演练演示如何创建一个出现在当前单词上的灯泡，并且有两个建议的操作：**转换为大写**，**转换为小写**。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建托管扩展框架 （MEF） 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`LightBulbTest`。

2. 向项目添加**编辑器分类器**项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 添加对项目的以下引用，并将 **"本地副本"** 设置为`False`：

     *Microsoft.VisualStudio.Language.Intellisense*

5. 添加新的类文件，并命名为**灯泡测试**。

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

1. 在*LightBulbTest.cs*类文件中，删除灯泡测试类。 添加一个名为**Test建议操作源提供程序**的类<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>，该提供程序实现 。 使用**测试建议操作**的名称和"文本"导出<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>它。

    ```csharp
    [Export(typeof(ISuggestedActionsSourceProvider))]
    [Name("Test Suggested Actions")]
    [ContentType("text")]
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider
    ```

2. 在源提供程序类中，导入<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>并将其添加为属性。

    ```csharp
    [Import(typeof(ITextStructureNavigatorSelectorService))]
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }
    ```

3. 实现返回<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A><xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>对象的方法。 下一节将讨论源。

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

## <a name="implement-the-isuggestedactionsource"></a>实施 I 建议操作源
 建议的操作源负责收集建议的操作集，并在正确的上下文中添加它们。 在这种情况下，上下文是当前单词，建议的操作是 **"大写建议操作"** 和 **"下Case建议操作"，** 下一节将对此进行讨论。

1. 添加实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>的类**Test 建议操作源**。

    ```csharp
    internal class TestSuggestedActionsSource : ISuggestedActionsSource
    ```

2. 为建议的操作源提供程序、文本缓冲区和文本视图添加专用的只读字段。

    ```csharp
    private readonly TestSuggestedActionsSourceProvider m_factory;
    private readonly ITextBuffer m_textBuffer;
    private readonly ITextView m_textView;
    ```

3. 添加设置私有字段的构造函数。

    ```csharp
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)
    {
        m_factory = testSuggestedActionsSourceProvider;
        m_textBuffer = textBuffer;
        m_textView = textView;
    }
    ```

4. 添加一个私有方法，用于返回当前位于光标下的单词。 以下方法查看光标的当前位置，并询问文本结构导航器单词的范围。 如果光标位于单词上，<xref:Microsoft.VisualStudio.Text.Operations.TextExtent>则在 out 参数中返回 。否则，`out`参数为`null`，该方法返回`false`。

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

5. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> 方法。 编辑器调用此方法以找出是否显示灯泡。 例如，每当光标从一行移动到另一行，或者当鼠标悬停在错误摆动上时，都会进行此调用。 它是异步的，以便允许在此方法工作时执行其他 UI 操作。 在大多数情况下，此方法需要对当前行执行一些分析和分析，因此处理可能需要一些时间。

     在此实现中，它异步获取<xref:Microsoft.VisualStudio.Text.Operations.TextExtent>并确定范围是否重要，如空格之外是否有文本。

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

6. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A>方法，该方法返回包含不同<xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet><xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>对象的对象数组。 当灯泡展开时，将调用此方法。

    > [!WARNING]
    > 应确保 和`HasSuggestedActionsAsync()``GetSuggestedActions()`的实现是一致的;也就是说，如果`HasSuggestedActionsAsync()`返回`true`，则`GetSuggestedActions()`应该有一些要显示的操作。 在许多情况下，`HasSuggestedActionsAsync()`在 之前调用`GetSuggestedActions()`，但情况并非总是如此。 例如，如果用户仅按 **（CTRL+** ）`GetSuggestedActions()`调用灯泡操作。

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

7. 定义事件`SuggestedActionsChanged`。

    ```csharp
    public event EventHandler<EventArgs> SuggestedActionsChanged;
    ```

8. 要完成实现，为`Dispose()``TryGetTelemetryId()`和 添加 实现。 您不想执行遥测，因此只需返回`false`并将 GUID 设置为`Empty`。

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

## <a name="implement-light-bulb-actions"></a>实施灯泡操作

1. 在项目中，添加对*Microsoft.VisualStudio.映像.Interop.14.0.DesignTime.dll 的*引用，并将 **"本地副本"** 设置为`False`。

2. 创建两个类，第一个名为 `UpperCaseSuggestedAction` ，第二个名为 `LowerCaseSuggestedAction`。 两个类都实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>。

    ```csharp
    internal class UpperCaseSuggestedAction : ISuggestedAction
    internal class LowerCaseSuggestedAction : ISuggestedAction
    ```

     这两个类相似，只不过其中一个调用 <xref:System.String.ToUpper%2A>，另一个调用 <xref:System.String.ToLower%2A>。 以下步骤仅说明大写操作类，但你必须实现这两个类。 将实现大写操作的步骤用作实现小写操作的模式。

3. 为这些类添加以下使用指令：

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

6. 实现该方法<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A>，以便显示操作预览。

    ```csharp
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)
    {
        var textBlock = new TextBlock();
        textBlock.Padding = new Thickness(5);
        textBlock.Inlines.Add(new Run() { Text = m_upper });
        return Task.FromResult<object>(textBlock);
    }
    ```

7. 实现该方法<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A>，以便返回空<xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet>枚举。

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
    > 灯泡操作 **"调用**"方法不应显示 UI。 如果操作确实带来了新的 UI（例如预览或选择对话框），请不要直接从**Invoke**方法中显示 UI，而是计划从**Invoke**返回后显示 UI。

10. 要完成实现，添加 和`Dispose()``TryGetTelemetryId()`方法。

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

11. 不要忘记`LowerCaseSuggestedAction`做同样的事情，将显示文本更改为"转换'{0}到小写"，并调用<xref:System.String.ToUpper%2A><xref:System.String.ToLower%2A>。

## <a name="build-and-test-the-code"></a>生成和测试代码
 要测试此代码，请构建灯泡测试解决方案并在实验实例中运行它。

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本。 您应该看到文本左侧的灯泡。

     ![测试灯泡](../extensibility/media/testlightbulb.png "测试LIghtBulb")

4. 指向灯泡。 您应该会看到一个向下箭头。

5. 单击灯泡时，应显示两个建议的操作以及所选操作的预览。

     ![测试灯泡，已展开](../extensibility/media/testlightbulbexpanded.gif "TestLIghtBulb 扩展")

6. 如果单击第一个操作，则当前单词中的所有文本都应转换为大写。 如果单击第二个操作，则所有文本都应转换为小写。
