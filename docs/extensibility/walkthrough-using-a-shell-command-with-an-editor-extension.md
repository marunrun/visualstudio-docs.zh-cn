---
title: 演练：使用具有编辑器扩展的 Shell 命令 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - add a menu command
ms.assetid: 08526848-a442-4cd4-afa1-b2eac2005adb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 52b151b09c1bb7306b4270f9408d0f04a7600aa2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697166"
---
# <a name="walkthrough-use-a-shell-command-with-an-editor-extension"></a>演练：使用具有编辑器扩展的 shell 命令
从 VSPackage 中，您可以将菜单命令等功能添加到编辑器中。 本演练演示如何通过调用菜单命令向编辑器中的文本视图添加修饰。

 本演练演示了 VSPackage 与托管扩展性框架 （MEF） 组件部件的使用。 您必须使用 VSPackage 将菜单命令注册到 Visual Studio 外壳。 而且，您可以使用 该命令访问 MEF 组件部件。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展
 创建 VSPackage，将名为"**添加修饰"** 的菜单命令放在 **"工具"** 菜单上。

1. 创建名为 的`MenuCommandTest`C# VSIX 项目，并添加自定义命令项模板名称**Addadornment**。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 将打开名为 MenuCommandTest 的解决方案。 MenuCommandTestPackage 文件具有创建菜单命令并将其放在 **"工具"** 菜单上的代码。 此时，该命令只是导致出现消息框。 后续步骤将演示如何更改此功能以显示注释修饰。

3. 打开 VSIX 清单编辑器中的*源.扩展.vsix清单*文件。 该`Assets`选项卡应具有 Microsoft 的行。

4. 保存并关闭*源.扩展.vsixmanifest*文件。

## <a name="add-a-mef-extension-to-the-command-extension"></a>向命令扩展添加 MEF 扩展

1. 在 **"解决方案资源管理器"** 中，右键单击解决方案节点，单击"**添加**"，然后单击 **"新项目**"。 在"**添加新项目"** 对话框中，单击**Visual C#** 下的 **"扩展性**"，然后单击**VSIX 项目**。 将项目命名为 `CommentAdornmentTest`。

2. 由于此项目将与强命名的 VSPackage 程序集进行交互，因此必须对程序集进行签名。 您可以重用为 VSPackage 程序集创建的密钥文件。

    1. 打开项目属性并选择"**签名**"选项卡。

    2. 选择**对程序集进行签名**。

    3. 在 **"选择强名称密钥文件**"下，选择为 MenuCommandTest 程序集生成的*Key.snk*文件。

## <a name="refer-to-the-mef-extension-in-the-vspackage-project"></a>请参阅 VSPackage 项目中的 MEF 扩展
 由于要向 VSPackage 添加 MEF 组件，因此必须在清单中指定这两种资产。

> [!NOTE]
> 有关 MEF 的详细信息，请参阅[托管扩展性框架 （MEF）。](/dotnet/framework/mef/index)

### <a name="to-refer-to-the-mef-component-in-the-vspackage-project"></a>在 VSPackage 项目中引用 MEF 组件

1. 在 MenuCommandTest 项目中，在 VSIX 清单编辑器中打开*源.扩展.vsix清单*文件。

2. 在"**资产**"选项卡上，单击 **"新建**"。

3. 在 **"类型"** 列表中，选择**Microsoft.VisualStudio.Mef组件**。

4. 在 **"源"** 列表中，选择**当前解决方案中的项目**。

5. 在 **"项目**"列表中，选择**注释验证测试**。

6. 保存并关闭*源.扩展.vsixmanifest*文件。

7. 确保 MenuCommandTest 项目具有对注释验证测试项目的引用。

8. 在注释注释测试项目中，将项目设置为生成程序集。 在**解决方案资源管理器**中，选择项目并在"**将生成输出复制到输出目录**"**属性**的属性窗口中查找，并将其设置为**true**。

## <a name="define-a-comment-adornment"></a>定义注释修饰
 注释修饰本身由跟踪所选文本的<xref:Microsoft.VisualStudio.Text.ITrackingSpan>和一些表示作者和文本描述的字符串组成。

#### <a name="to-define-a-comment-adornment"></a>定义注释修饰

1. 在注释验证测试中，添加新的类文件并将其命名为`CommentAdornment`。

2. 添加以下引用：

    1. 微软.VisualStudio.核心实用程序

    2. 微软.VisualStudio.文本.数据

    3. 微软.VisualStudio.文本.逻辑

    4. 微软.VisualStudio.文本.UI

    5. 微软.VisualStudio.文本.UI.Wpf

    6. System.ComponentModel.Composition

    7. PresentationCore

    8. PresentationFramework

    9. WindowsBase

3. 添加以下`using`指令。

    ```csharp
    using Microsoft.VisualStudio.Text;
    ```

4. 该文件应包含名为 的`CommentAdornment`类。

    ```csharp
    internal class CommentAdornment
    ```

5. 将三个字段添加到`CommentAdornment`<xref:Microsoft.VisualStudio.Text.ITrackingSpan>的类 中，作者和说明。

    ```csharp
    public readonly ITrackingSpan Span;
    public readonly string Author;
    public readonly string Text;
    ```

6. 添加初始化字段的构造函数。

    ```csharp
    public CommentAdornment(SnapshotSpan span, string author, string text)
    {
        this.Span = span.Snapshot.CreateTrackingSpan(span, SpanTrackingMode.EdgeExclusive);
        this.Author = author;
        this.Text = text;
    }
    ```

## <a name="create-a-visual-element-for-the-adornment"></a>为修饰创建可视元素
 为修饰定义可视元素。 在本演练中，定义从 Windows 演示文稿基础 （WPF） 类<xref:System.Windows.Controls.Canvas>继承的控件。

1. 在注释验证测试中创建一个类，并命名它`CommentBlock`。

2. 添加以下`using`指令。

    ```csharp
    using Microsoft.VisualStudio.Text;
    using System;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Media;
    using System.Windows.Shapes;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. 使`CommentBlock`类从<xref:System.Windows.Controls.Canvas>继承。

    ```csharp
    internal class CommentBlock : Canvas
    { }
    ```

4. 添加一些私有字段以定义修饰的视觉方面。

    ```csharp
    private Geometry textGeometry;
    private Grid commentGrid;
    private static Brush brush;
    private static Pen solidPen;
    private static Pen dashPen;
    ```

5. 添加定义注释修饰并添加相关文本的构造函数。

    ```csharp
    public CommentBlock(double textRightEdge, double viewRightEdge,
            Geometry newTextGeometry, string author, string body)
    {
        if (brush == null)
        {
            brush = new SolidColorBrush(Color.FromArgb(0x20, 0x00, 0xff, 0x00));
            brush.Freeze();
            Brush penBrush = new SolidColorBrush(Colors.Green);
            penBrush.Freeze();
            solidPen = new Pen(penBrush, 0.5);
            solidPen.Freeze();
            dashPen = new Pen(penBrush, 0.5);
            dashPen.DashStyle = DashStyles.Dash;
            dashPen.Freeze();
        }

        this.textGeometry = newTextGeometry;

        TextBlock tb1 = new TextBlock();
        tb1.Text = author;
        TextBlock tb2 = new TextBlock();
        tb2.Text = body;

        const int MarginWidth = 8;
        this.commentGrid = new Grid();
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        ColumnDefinition cEdge = new ColumnDefinition();
        cEdge.Width = new GridLength(MarginWidth);
        ColumnDefinition cEdge2 = new ColumnDefinition();
        cEdge2.Width = new GridLength(MarginWidth);
        this.commentGrid.ColumnDefinitions.Add(cEdge);
        this.commentGrid.ColumnDefinitions.Add(new ColumnDefinition());
        this.commentGrid.ColumnDefinitions.Add(cEdge2);

        System.Windows.Shapes.Rectangle rect = new System.Windows.Shapes.Rectangle();
        rect.RadiusX = 6;
        rect.RadiusY = 3;
        rect.Fill = brush;
        rect.Stroke = Brushes.Green;

            Size inf = new Size(double.PositiveInfinity, double.PositiveInfinity);
            tb1.Measure(inf);
            tb2.Measure(inf);
            double middleWidth = Math.Max(tb1.DesiredSize.Width, tb2.DesiredSize.Width);
            this.commentGrid.Width = middleWidth + 2 * MarginWidth;

        Grid.SetColumn(rect, 0);
        Grid.SetRow(rect, 0);
        Grid.SetRowSpan(rect, 2);
        Grid.SetColumnSpan(rect, 3);
        Grid.SetRow(tb1, 0);
        Grid.SetColumn(tb1, 1);
        Grid.SetRow(tb2, 1);
        Grid.SetColumn(tb2, 1);
        this.commentGrid.Children.Add(rect);
        this.commentGrid.Children.Add(tb1);
        this.commentGrid.Children.Add(tb2);

        Canvas.SetLeft(this.commentGrid, Math.Max(viewRightEdge - this.commentGrid.Width - 20.0, textRightEdge + 20.0));
        Canvas.SetTop(this.commentGrid, textGeometry.GetRenderBounds(solidPen).Top);

        this.Children.Add(this.commentGrid);
    }
    ```

6. 还实现绘制<xref:System.Windows.Controls.Panel.OnRender%2A>修饰的事件处理程序。

    ```csharp
    protected override void OnRender(DrawingContext dc)
    {
        base.OnRender(dc);
        if (this.textGeometry != null)
        {
            dc.DrawGeometry(brush, solidPen, this.textGeometry);
            Rect textBounds = this.textGeometry.GetRenderBounds(solidPen);
            Point p1 = new Point(textBounds.Right, textBounds.Bottom);
            Point p2 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid) - 20.0, p1.X), p1.Y);
            Point p3 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid), p1.X), (Canvas.GetTop(this.commentGrid) + p1.Y) * 0.5);
            dc.DrawLine(dashPen, p1, p2);
            dc.DrawLine(dashPen, p2, p3);
        }
    }
    ```

## <a name="add-an-iwpftextviewcreationlistener"></a>添加 IWpftext 视图创建侦听器
 是<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>MEF 组件部分，可用于侦听创建事件。

1. 将类文件添加到注释修饰测试项目并将其命名为`Connector`。

2. 添加以下`using`指令。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. 声明实现<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>的类，并将其导出为<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"text"和<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute><xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>a。 内容类型属性指定组件应用于的内容类型。 文本类型是所有非二进制文件类型的基础类型。 因此，创建的几乎每个文本视图都将是此类型。 文本视图角色属性指定组件应用于的文本视图类型。 文档文本视图角色通常显示由行组成并存储在文件中的文本。

     [!code-vb[VSSDKMenuCommandTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_1.vb)]
     [!code-csharp[VSSDKMenuCommandTest#11](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_1.cs)]

4. 实现<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>该方法，以便调用 的`Create()``CommentAdornmentManager`静态事件。

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        CommentAdornmentManager.Create(textView);
    }
    ```

5. 添加可用于执行命令的方法。

    ```csharp
    static public void Execute(IWpfTextViewHost host)
    {
        IWpfTextView view = host.TextView;
        //Add a comment on the selected text. 
        if (!view.Selection.IsEmpty)
        {
            //Get the provider for the comment adornments in the property bag of the view.
            CommentAdornmentProvider provider = view.Properties.GetProperty<CommentAdornmentProvider>(typeof(CommentAdornmentProvider));

            //Add some arbitrary author and comment text. 
            string author = System.Security.Principal.WindowsIdentity.GetCurrent().Name;
            string comment = "Four score....";

            //Add the comment adornment using the provider.
            provider.Add(view.Selection.SelectedSpans[0], author, comment);
        }
    }
    ```

## <a name="define-an-adornment-layer"></a>定义修饰图层
 要添加新修饰，必须定义修饰图层。

### <a name="to-define-an-adornment-layer"></a>定义修饰图层

1. 在`Connector`类中，声明类型<xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition>的公共字段，并将其导出为<xref:Microsoft.VisualStudio.Utilities.NameAttribute>指定修饰图层的唯一名称，以及<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>定义此修饰图层的 Z 顺序关系到其他文本视图图层（文本、缀和选择） 的字段。

    ```csharp
    [Export(typeof(AdornmentLayerDefinition))]
    [Name("CommentAdornmentLayer")]
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
    public AdornmentLayerDefinition commentLayerDefinition;

    ```

## <a name="provide-comment-adornments"></a>提供注释修饰
 定义修饰时，还实现注释修饰提供程序和注释修饰管理器。 注释修饰提供程序保留注释修饰列表，侦听<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>基础文本缓冲区上的事件，并在删除基础文本时删除注释修饰。

1. 将新的类文件添加到注释修饰测试项目并将其命名为`CommentAdornmentProvider`。

2. 添加以下`using`指令。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Collections.ObjectModel;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    ```

3. 添加名为的 `CommentAdornmentProvider` 的类。

    ```csharp
    internal class CommentAdornmentProvider
    {
    }
    ```

4. 为文本缓冲区添加私有字段以及与缓冲区相关的注释修饰列表。

    ```csharp
    private ITextBuffer buffer;
    private IList<CommentAdornment> comments = new List<CommentAdornment>();

    ```

5. 添加`CommentAdornmentProvider`的构造函数。 此构造函数应具有私有访问权限，因为提供程序由`Create()`方法实例化。 构造函数将`OnBufferChanged`事件处理程序添加到事件<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>。

    ```csharp
    private CommentAdornmentProvider(ITextBuffer buffer)
    {
        this.buffer = buffer;
        //listen to the Changed event so we can react to deletions. 
        this.buffer.Changed += OnBufferChanged;
    }

    ```

6. 添加 `Create()` 方法。

    ```csharp
    public static CommentAdornmentProvider Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentProvider>(delegate { return new CommentAdornmentProvider(view.TextBuffer); });
    }

    ```

7. 添加 `Detach()` 方法。

    ```csharp
    public void Detach()
    {
        if (this.buffer != null)
        {
            //remove the Changed listener 
            this.buffer.Changed -= OnBufferChanged;
            this.buffer = null;
        }
    }
    ```

8. 添加事件`OnBufferChanged`处理程序。

     [!code-csharp[VSSDKMenuCommandTest#21](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_2.cs)]
     [!code-vb[VSSDKMenuCommandTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_2.vb)]

9. 添加`CommentsChanged`事件的声明。

    ```csharp
    public event EventHandler<CommentsChangedEventArgs> CommentsChanged;
    ```

10. 创建一`Add()`个方法来添加修饰。

    ```csharp
    public void Add(SnapshotSpan span, string author, string text)
    {
        if (span.Length == 0)
            throw new ArgumentOutOfRangeException("span");
        if (author == null)
            throw new ArgumentNullException("author");
        if (text == null)
            throw new ArgumentNullException("text");

        //Create a comment adornment given the span, author and text.
        CommentAdornment comment = new CommentAdornment(span, author, text);

        //Add it to the list of comments. 
        this.comments.Add(comment);

        //Raise the changed event.
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;
        if (commentsChanged != null)
            commentsChanged(this, new CommentsChangedEventArgs(comment, null));
    }

    ```

11. 添加方法`RemoveComments()`。

    ```csharp
    public void RemoveComments(SnapshotSpan span)
    {
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;

        //Get a list of all the comments that are being kept
        IList<CommentAdornment> keptComments = new List<CommentAdornment>(this.comments.Count);

        foreach (CommentAdornment comment in this.comments)
        {
            //find out if the given span overlaps with the comment text span. If two spans are adjacent, they do not overlap. To consider adjacent spans, use IntersectsWith. 
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
            {
                //Raise the change event to delete this comment. 
                if (commentsChanged != null)
                    commentsChanged(this, new CommentsChangedEventArgs(null, comment));
            }
            else
                keptComments.Add(comment);
        }

        this.comments = keptComments;
    }
    ```

12. 添加一`GetComments()`个方法，返回给定快照范围内的所有注释。

    ```csharp
    public Collection<CommentAdornment> GetComments(SnapshotSpan span)
    {
        IList<CommentAdornment> overlappingComments = new List<CommentAdornment>();
        foreach (CommentAdornment comment in this.comments)
        {
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
                overlappingComments.Add(comment);
        }

        return new Collection<CommentAdornment>(overlappingComments);
    }
    ```

13. 添加名为 的`CommentsChangedEventArgs`类，如下所示。

    ```csharp
    internal class CommentsChangedEventArgs : EventArgs
    {
        public readonly CommentAdornment CommentAdded;

        public readonly CommentAdornment CommentRemoved;

        public CommentsChangedEventArgs(CommentAdornment added, CommentAdornment removed)
        {
            this.CommentAdded = added;
            this.CommentRemoved = removed;
        }
    }
    ```

## <a name="manage-comment-adornments"></a>管理注释修饰
 注释修饰管理器创建修饰并将其添加到修饰层。 它侦听<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>和<xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed>事件，以便可以移动或删除修饰。 它还侦听添加或删除注释`CommentsChanged`时注释修饰提供程序触发的事件。

1. 将类文件添加到注释修饰测试项目并将其命名为`CommentAdornmentManager`。

2. 添加以下`using`指令。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Windows.Media;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Formatting;
    ```

3. 添加名为的 `CommentAdornmentManager` 的类。

    ```csharp
    internal class CommentAdornmentManager
        {
        }
    ```

4. 添加一些私有字段。

    ```csharp
    private readonly IWpfTextView view;
    private readonly IAdornmentLayer layer;
    private readonly CommentAdornmentProvider provider;
    ```

5. 添加将管理器订阅<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>到 和<xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed>事件以及事件的`CommentsChanged`构造函数。 构造函数是私有的，因为管理器由静态`Create()`方法实例化。

    ```csharp
    private CommentAdornmentManager(IWpfTextView view)
    {
        this.view = view;
        this.view.LayoutChanged += OnLayoutChanged;
        this.view.Closed += OnClosed;

        this.layer = view.GetAdornmentLayer("CommentAdornmentLayer");

        this.provider = CommentAdornmentProvider.Create(view);
        this.provider.CommentsChanged += OnCommentsChanged;
    }
    ```

6. 添加获取`Create()`提供程序的方法，或在必要时创建提供程序。

    ```csharp
    public static CommentAdornmentManager Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentManager>(delegate { return new CommentAdornmentManager(view); });
    }
    ```

7. 添加`CommentsChanged`处理程序。

    ```csharp
    private void OnCommentsChanged(object sender, CommentsChangedEventArgs e)
    {
        //Remove the comment (when the adornment was added, the comment adornment was used as the tag). 
        if (e.CommentRemoved != null)
            this.layer.RemoveAdornmentsByTag(e.CommentRemoved);

        //Draw the newly added comment (this will appear immediately: the view does not need to do a layout). 
        if (e.CommentAdded != null)
            this.DrawComment(e.CommentAdded);
    }
    ```

8. 添加<xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed>处理程序。

    ```csharp
    private void OnClosed(object sender, EventArgs e)
    {
        this.provider.Detach();
        this.view.LayoutChanged -= OnLayoutChanged;
        this.view.Closed -= OnClosed;
    }
    ```

9. 添加<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>处理程序。

    ```csharp
    private void OnLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        //Get all of the comments that intersect any of the new or reformatted lines of text.
        List<CommentAdornment> newComments = new List<CommentAdornment>();

        //The event args contain a list of modified lines and a NormalizedSpanCollection of the spans of the modified lines.  
        //Use the latter to find the comments that intersect the new or reformatted lines of text. 
        foreach (Span span in e.NewOrReformattedSpans)
        {
            newComments.AddRange(this.provider.GetComments(new SnapshotSpan(this.view.TextSnapshot, span)));
        }

        //It is possible to get duplicates in this list if a comment spanned 3 lines, and the first and last lines were modified but the middle line was not. 
        //Sort the list and skip duplicates.
        newComments.Sort(delegate(CommentAdornment a, CommentAdornment b) { return a.GetHashCode().CompareTo(b.GetHashCode()); });

        CommentAdornment lastComment = null;
        foreach (CommentAdornment comment in newComments)
        {
            if (comment != lastComment)
            {
                lastComment = comment;
                this.DrawComment(comment);
            }
        }
    }
    ```

10. 添加绘制注释的私有方法。

     [!code-csharp[VSSDKMenuCommandTest#35](../extensibility/codesnippet/CSharp/walkthrough-using-a-shell-command-with-an-editor-extension_3.cs)]
     [!code-vb[VSSDKMenuCommandTest#35](../extensibility/codesnippet/VisualBasic/walkthrough-using-a-shell-command-with-an-editor-extension_3.vb)]

## <a name="use-the-menu-command-to-add-the-comment-adornment"></a>使用菜单命令添加注释修饰
 您可以使用菜单命令通过实现 VSPackage`MenuItemCallback`的方法来创建注释修饰。

1. 向菜单命令测试项目添加以下引用：

    - 微软.VisualStudio.文本管理器.互通

    - 微软.VisualStudio.编辑器

    - 微软.VisualStudio.文本.UI.Wpf

2. 打开*AddAdornment.cs*文件并添加以下`using`指令。

    ```csharp
    using Microsoft.VisualStudio.TextManager.Interop;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Editor;
    using CommentAdornmentTest;
    ```

3. 删除`Execute()`方法并添加以下命令处理程序。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
    }
    ```

4. 添加代码以获取活动视图。 您必须获取`SVsTextManager`视觉工作室外壳才能激活`IVsTextView`。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
    }
    ```

5. 如果此文本视图是编辑器文本视图的实例，则可以将其转换为接口，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>然后获取<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>及其关联的<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>。 使用<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>调用`Connector.Execute()`方法，该方法获取注释修饰提供程序并添加修饰。 命令处理程序现在应如下所示：

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
        IVsUserData userData = vTextView as IVsUserData;
         if (userData == null)
        {
            Console.WriteLine("No text view is currently open");
            return;
        }
        IWpfTextViewHost viewHost;
        object holder;
        Guid guidViewHost = DefGuidList.guidIWpfTextViewHost;
        userData.GetData(ref guidViewHost, out holder);
        viewHost = (IWpfTextViewHost)holder;
        Connector.Execute(viewHost);
    }
    ```

6. 将 AddAdornmentHandler 方法设置为 AddAdornment 构造函数中 AddAdornment 命令的处理程序。

    ```csharp
    private AddAdornment(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        var menuCommandID = new CommandID(CommandSet, CommandId);
        var menuItem = new MenuCommand(this.AddAdornmentHandler, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

## <a name="build-and-test-the-code"></a>生成和测试代码

1. 生成解决方案并启动调试。 应出现实验实例。

2. 创建文本文件。 键入某些文本，然后选择它。

3. 在 **"工具"** 菜单上，单击 **"调用添加修饰**"。 气球应显示在文本窗口的右侧，并且应包含类似于以下文本的文本。

     您的用户名

     四分...

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
