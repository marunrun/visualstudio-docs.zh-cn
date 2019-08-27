---
title: 演练：显示灯泡建议 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f135247241e8cf441cba2c1f63984dc69f7114c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438148"
---
# <a name="walkthrough-displaying-light-bulb-suggestions"></a>演练：显示灯泡建议
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

电灯泡是 Visual Studio 编辑器中使用的图标，展开此项可显示的一组操作，例如通过内置的代码分析器或重构代码标识的问题的修补程序。  
  
 在 Visual C# 和 Visual Basic 编辑器中，您还可以使用.NET 编译器平台 ("Roslyn") 编写并打包你自己的自动显示灯泡的操作的代码分析器。 有关详细信息，请参见:  
  
- [如何：编写C#诊断和代码修补程序](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)  
  
- [如何：编写 Visual Basic 诊断和代码修补程序](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix)  
  
  其他语言，如C++还提供一些快速操作，如创建该函数的存根 （stub） 实现建议灯泡。  
  
  下面是一个灯泡如下所示。 在 Visual Basic 或 Visual C# 项目中，红色曲线将显示在变量名称下时是无效的。 当您将鼠标移到无效的标识符时，在光标附近将显示灯泡。  
  
  ![灯泡](../extensibility/media/lightbulb.png "灯泡图标")  
  
  如果通过灯泡图标中单击向下箭头，将显示一组建议的操作，以及所选操作的预览。 在这种情况下，它显示如果执行该操作将对你的代码的更改。  
  
  ![灯泡预览](../extensibility/media/lightbulbpreview.png "LightBulbPreview")  
  
  可以使用灯泡提供建议的操作。 例如，您可以提供要移动打开到新行的大括号或将它们移动到上一行末尾的操作。 下面的演练演示如何创建将显示一个灯泡在当前单词上并且具有两个建议操作：**将转换为大写**并**转换为小写**。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目  
  
1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `LightBulbTest`。  
  
2. 添加**编辑器分类器**到项目项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 删除现有的类文件。  
  
4. 添加以下引用到项目中，并设置**Copy Local**到`False`:  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
5. 添加一个新类文件并将其命名**LightBulbTest**。  
  
6. 添加以下 using 语句：  
  
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
  
## <a name="implementing-the-light-bulb-source-provider"></a>实现灯泡源提供程序  
  
1. 在 LightBulbTest.cs 类文件中，删除 LightBulbTest 类。 添加名为的类**TestSuggestedActionsSourceProvider**实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>。 使用的名称将其导出**测试建议的操作**和一个<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"text"。  
  
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
  
3. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A>方法以返回<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>对象。 我们将讨论下一节中的源。  
  
    ```csharp  
    public ISuggestedActionsSource CreateSuggestedActionsSource(ITextView textView, ITextBuffer textBuffer)  
    {  
        if (textBuffer == null && textView == null)  
        {  
            return null;  
        }  
        return new TestSuggestedActionsSource(this, textView, textBuffer);  
    }  
    ```  
  
## <a name="implementing-the-isuggestedactionsource"></a>实现 ISuggestedActionSource  
 建议的操作源负责收集的一套建议的操作并将其添加在正确的环境。 在这种情况下的上下文是当前的单词和建议的操作都**UpperCaseSuggestedAction**和**LowerCaseSuggestedAction**，我们将讨论下一节中。  
  
1. 将类添加**TestSuggestedActionsSource**实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>。  
  
    ```csharp  
    internal class TestSuggestedActionsSource : ISuggestedActionsSource  
    ```  
  
2. 建议的操作源提供程序、 文本缓冲区和文本视图中添加专用的只读字段。  
  
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
  
4. 添加一个私有方法返回当前光标下的单词。 以下方法看起来在光标的当前位置，并要求提供的字范围文本结构导航器。 如果光标在字词<xref:Microsoft.VisualStudio.Text.Operations.TextExtent>输出参数中返回; 否则为`out`参数是`null`并且该方法返回`false`。  
  
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
  
5. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> 方法。 编辑器中调用此方法来找出是否显示灯泡图标中。 进行此调用可能经常例如只要将光标从一个行移动到另一个，或者当鼠标悬停在该错误曲线。 它是为了允许使用此方法时执行其他 UI 操作异步的。 在大多数情况下，此方法需要对其执行某些分析和分析的当前行，因此在处理可能需要一些时间。  
  
     在我们的实现它以异步方式获取<xref:Microsoft.VisualStudio.Text.Operations.TextExtent>并确定范围是否有效，即它是否有一些文本，而不是空格。  
  
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
  
6. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A>方法，返回的数组<xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet>包含不同的对象<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>对象。 灯泡图标展开时，调用此方法。  
  
    > [!WARNING]
    > 应确保的实现`HasSuggestedActionsAsync()`并`GetSuggestedActions()`是否一致; 即，如果`HasSuggestedActionsAsync()`返回`true`，然后`GetSuggestedActions()`应具有某些操作来显示。 在许多情况下`HasSuggestedActionsAsync()`之前调用`GetSuggestedActions()`，但并不总是这种情况。 例如，如果用户通过按调用灯泡操作 (CTRL +。) 仅`GetSuggestedActions()`调用。  
  
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
  
7. 定义`SuggestedActionsChanged`事件。  
  
    ```csharp  
    public event EventHandler<EventArgs> SuggestedActionsChanged;  
    ```  
  
8. 若要完成实现，添加实现`Dispose()`和`TryGetTelemetryId()`方法。 我们不希望执行遥测数据，因此只返回 false 并将 GUID 设置为空。  
  
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
  
## <a name="implementing-light-bulb-actions"></a>实现灯泡操作  
  
1. 在项目中，添加对 Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll 并集的引用**Copy Local**到`False`。  
  
2. 创建两个类，第一个名为 `UpperCaseSuggestedAction` ，第二个名为 `LowerCaseSuggestedAction`。 两个类都实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction>。  
  
    ```csharp  
    internal class UpperCaseSuggestedAction : ISuggestedAction   
    internal class LowerCaseSuggestedAction : ISuggestedAction  
    ```  
  
     这两个类相似，只不过其中一个调用 <xref:System.String.ToUpper%2A>，另一个调用 <xref:System.String.ToLower%2A>。 以下步骤仅说明大写操作类，但你必须实现这两个类。 将实现大写操作的步骤用作实现小写操作的模式。  
  
3. 添加以下 using 语句，这些类：  
  
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
  
6. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A>方法，以便它显示在操作预览。  
  
    ```csharp  
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)  
    {  
        var textBlock = new TextBlock();  
        textBlock.Padding = new Thickness(5);  
        textBlock.Inlines.Add(new Run() { Text = m_upper });  
        return Task.FromResult<object>(textBlock);  
    }  
    ```  
  
7. 实现<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A>方法，以便它返回一个空<xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet>枚举。  
  
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
    > 灯泡菜单操作**Invoke**方法不应显示 UI。  如果你的操作会带来新的用户界面 （例如预览或选择对话框），不会显示直接从用户界面**Invoke**方法，但改为计划从返回之后显示 UI **Invoke**.  
  
10. 若要完成实现，添加`Dispose()`和`TryGetTelemetryId()`方法。  
  
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
  
11. 别忘了执行相同的操作`LowerCaseSuggestedAction`更改为显示文本"转换{0}为小写"，并调用<xref:System.String.ToUpper%2A>到<xref:System.String.ToLower%2A>。  
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
 若要测试此代码，生成 LightBulbTest 解决方案并在实验实例中运行它。  
  
1. 生成解决方案。  
  
2. 在调试器中运行此项目时，Visual Studio 的第二个实例将进行实例化。  
  
3. 创建一个文本文件并键入一些文本。 应会看到文本的左侧的灯泡。  
  
     ![测试灯泡](../extensibility/media/testlightbulb.png "TestLIghtBulb")  
  
4. 指向灯泡图标中。 应看到向下箭头。  
  
5. 当您单击灯泡图标中时，两个建议的操作应显示，以及所选操作的预览。  
  
     ![测试灯泡已展开](../extensibility/media/testlightbulbexpanded.gif "TestLIghtBulbExpanded")  
  
6. 如果单击第一个操作，则当前单词中的所有文本都将转换为大写。 如果单击第二个操作，则所有文本都将转换为小写。
