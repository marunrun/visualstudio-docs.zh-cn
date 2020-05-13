---
title: 扩展属性、任务列表、输出、选项窗口
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- properties pane
- task list
- output window
- properties window
- tutorials
- tool windows
ms.assetid: 06990510-5424-44b8-9fd9-6481acec5c76
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: db14068c97ff6868f5fb73c9ddd790020e99e7c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711634"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>扩展属性、任务列表、输出和选项窗口
您可以访问可视化工作室中的任何工具窗口。 本演练演示如何将有关工具窗口的信息集成到新的 **"选项"** 页和 **"属性**"页上的新设置中，以及如何写入**任务列表**和**输出**窗口。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

1. 使用 VSIX 模板创建名为**TodoList**的项目，并添加名为**TodoWindow**的自定义工具窗口项模板。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="set-up-the-tool-window"></a>设置工具窗口
 添加用于键入新 ToDo 项的 TextBox、将新项目添加到列表中的按钮以及用于显示列表中项目的列表列表。

1. 在*TodoWindow.xaml*中 ，从用户控件中删除按钮、文本框和堆栈面板控件。

    > [!NOTE]
    > 这不会删除**button1_Click**事件处理程序，您将在后面的步骤中重用该处理程序。

2. 从**工具箱****的所有 WPF 控件**部分，将 **"画布"** 控件拖动到网格。

3. 将**文本框**、**按钮**和**列表框**拖动到画布。 排列元素，使 TextBox 和按钮位于同一级别，ListBox 将填充其下方的窗口的其余部分，如下图所示。

     ![已完成的工具窗口](../extensibility/media/t5-toolwindow.png "T5 工具窗口")

4. 在 XAML 窗格中，找到"按钮"并将其内容属性设置为 **"添加**"。 通过添加`Click="button1_Click"`属性将按钮事件处理程序重新连接到 Button 控件。 "画布"块应如下所示：

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>自定义构造函数

1. 在*TodoWindowControl.xaml.cs*文件中，添加以下使用指令：

    ```csharp
    using System;
    ```

2. 添加对 TodoWindow 的公共引用，并让 TodoWindow 控制构造函数采用 TodoWindow 参数。 代码应如下所示：

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. 在*TodoWindow.cs*中，更改 TodoWindow 控制构造函数以包括 TodoWindow 参数。 代码应如下所示：

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>创建选项页面
 您可以在"**选项"** 对话框中提供页面，以便用户可以更改工具窗口的设置。 创建选项页需要描述选项的类和*TodoListPackage.cs*或*TodoListPackage.vb*文件中的条目。

1. 添加名为的 `ToolsOptions.cs` 的类。 使`ToolsOptions`类从<xref:Microsoft.VisualStudio.Shell.DialogPage>继承。

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. 添加以下 using 指令：

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. 本演练中的"选项"页仅提供一个名为"天超"的选项。 向`ToolsOptions`类添加名为 **"天前"** 的私有字段和名为 **"天前"** 的属性：

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   现在，您必须使项目了解此选项页。

### <a name="make-the-options-page-available-to-users"></a>使选项页可供用户使用

1. 在*TodoWindowPackage.cs*中，<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>向`TodoWindowPackage`类添加 a：

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. ProvideOptionPage 构造函数的第一个参数是之前创建的类`ToolsOptions`的类型。 第二个参数"ToDo"是 **"选项"** 对话框中的类别名称。 第三个参数"常规"是 **"选项**"对话框的子类别的名称，其中"选项"页将可用。 接下来的两个参数是字符串的资源指示;另一个参数是字符串的资源指示。第一个是类别的名称，第二个是子类别的名称。 最终参数确定是否可以使用自动化访问此页面。

     当用户打开"选项"页时，它应类似于下图。

     ![“选项”页](../extensibility/media/t5optionspage.gif "T5选项页")

     请注意 **"DoDo"** 类别和子类别 **"常规**"。

## <a name="make-data-available-to-the-properties-window"></a>使数据可用于"属性"窗口
 您可以通过创建名为"ToDo"`TodoItem`列表中存储有关各个项的信息的类，使 ToDo 列表信息可用。

1. 添加名为的 `TodoItem.cs` 的类。

     当用户可以使用工具窗口时，ListBox 中的项目将由 TodoItems 表示。 当用户在 ListBox 中选择这些项目之一时，"**属性"** 窗口将显示有关该项目的信息。

     要使数据在 **"属性"** 窗口中可用，请将数据转换为具有两个特殊属性的公共属性和`Description``Category`。 `Description`是显示在 **"属性"** 窗口底部的文本。 `Category`确定**属性**在 **"分类"** 视图中显示时应显示的位置。 在下图中，"**属性"** 窗口位于 **"分类"** 视图中，选择了**ToDo 字段**类别中**的"名称**"属性，并且 **"名称"** 属性的说明显示在窗口底部。

     ![属性窗口](../extensibility/media/t5properties.png "T5属性")

2. 使用*TodoItem.cs*文件添加以下指令。

    ```csharp
    using System.ComponentModel;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. 将`public`访问修改器添加到类声明。

    ```csharp
    public class TodoItem
    {
    }
    ```

     添加两个属性`Name`和`DueDate`。 我们稍后再做`UpdateList()``CheckForErrors()`。

    ```csharp
    public class TodoItem
    {
        private TodoWindowControl parent;
        private string name;
        [Description("Name of the ToDo item")]
        [Category("ToDo Fields")]
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                parent.UpdateList(this);
            }
        }

        private DateTime dueDate;
        [Description("Due date of the ToDo item")]
        [Category("ToDo Fields")]
        public DateTime DueDate
        {
            get { return dueDate; }
            set
            {
                dueDate = value;
                parent.UpdateList(this);
                parent.CheckForErrors();
            }
        }
    }
    ```

4. 向用户控件添加私有引用。 添加一个构造函数，该构造函数获取此 ToDo 项的用户控件和名称。 要查找 的值`daysAhead`，它获取"选项"页属性。

    ```csharp
    private TodoWindowControl parent;

    public TodoItem(TodoWindowControl control, string itemName)
    {
        parent = control;
        name = itemName;
        dueDate = DateTime.Now;

        double daysAhead = 0;
        IVsPackage package = parent.parent.Package as IVsPackage;
        if (package != null)
        {
            object obj;
            package.GetAutomationObject("ToDo.General", out obj);

            ToolsOptions options = obj as ToolsOptions;
            if (options != null)
            {
                daysAhead = options.DaysAhead;
            }
        }

        dueDate = dueDate.AddDays(daysAhead);
    }
    ```

5. 由于类的`TodoItem`实例将存储在 ListBox 中，ListBox 将调用`ToString`该函数，因此必须重载`ToString`函数。 在构造函数之后和类结束之前将以下代码添加到*TodoItem.cs*。。

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. 在*TodoWindowControl.xaml.cs*中，将存根`TodoWindowControl`方法添加到`CheckForError`和`UpdateList`方法的类中。 将它们放在进程对话查尔之后和文件结束之前。

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     该方法`CheckForError`将调用父对象中具有相同名称的方法，该方法将检查是否发生了任何错误并正确处理它们。 该方法`UpdateList`将更新父控件中的 ListBox;当 类 中的`Name`和`DueDate`属性发生更改时，将调用 方法。 稍后将实施。

## <a name="integrate-into-the-properties-window"></a>集成到"属性"窗口中
 现在编写管理 ListBox 的代码，该代码将绑定到 **"属性"** 窗口。

 您必须更改按钮单击处理程序才能读取文本框、创建 TodoItem 并将其添加到 ListBox。

1. 将现有`button1_Click`函数替换为创建新 TodoItem 并将其添加到 ListBox 的代码。 它调用`TrackSelection()`，稍后将定义。

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. 在"设计"视图中选择"列表框"控件。 在"**属性"** 窗口中单击 **"事件处理程序"** 按钮，然后查找 **"选择更改"** 事件。 用**listBox_SelectionChanged**填写文本框。 执行此操作会为选择更改处理程序添加一个存根，并将其分配给事件。

3. 实现 `TrackSelection()` 方法。 由于您需要获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell><xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>服务，因此需要通过 TodoWindowControl<xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A>进行访问。 将以下方法添加到 `TodoWindow` 类：

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. 将以下使用指令添加到*TodoWindowControl.xaml.cs*：

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. 填写"选择更改"处理程序，如下所示：

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. 现在，填写"轨道选择"功能，该函数将提供与 **"属性"** 窗口的集成。 当用户将项目添加到 ListBox 或单击 ListBox 中的项目时，将调用此功能。 它将 ListBox 的内容添加到选择容器，并将选择容器传递到**属性**窗口<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>的事件处理程序。 "轨迹选择"服务跟踪用户界面 （UI） 中的选定对象并显示其属性

    ```csharp
    private SelectionContainer mySelContainer;
    private System.Collections.ArrayList mySelItems;
    private IVsWindowFrame frame = null;

    private void TrackSelection()
    {
        if (frame == null)
        {
            var shell = parent.GetVsService(typeof(SVsUIShell)) as IVsUIShell;
            if (shell != null)
            {
                var guidPropertyBrowser = new
                Guid(ToolWindowGuids.PropertyBrowser);
                shell.FindToolWindow((uint)__VSFINDTOOLWIN.FTW_fForceCreate,
                ref guidPropertyBrowser, out frame);
            }
        }
        if (frame != null)
            {
                frame.Show();
            }
        if (mySelContainer == null)
        {
            mySelContainer = new SelectionContainer();
        }

        mySelItems = new System.Collections.ArrayList();

        var selected = listBox.SelectedItem as TodoItem;
        if (selected != null)
        {
            mySelItems.Add(selected);
        }

        mySelContainer.SelectedObjects = mySelItems;

        ITrackSelection track = parent.GetVsService(typeof(STrackSelection))
                                as ITrackSelection;
        if (track != null)
        {
            track.OnSelectChange(mySelContainer);
        }
    }
    ```

     现在，您拥有了 **"属性"** 窗口可以使用的类，则可以将 **"属性"** 窗口与工具窗口集成。 当用户单击工具窗口中的 ListBox 中的项目时，"**属性"** 窗口应相应地更新。 同样，当用户在"**属性"** 窗口中更改 ToDo 项时，应更新关联的项。

7. 现在，在*TodoWindowControl.xaml.cs*中添加 UpdateList 函数代码的其余部分。 它应该从 ListBox 中删除并重新添加修改后的 TodoItem。

    ```csharp
    public void UpdateList(TodoItem item)
    {
        var index = listBox.SelectedIndex;
        listBox.Items.RemoveAt(index);
        listBox.Items.Insert(index, item);
        listBox.SelectedItem = index;
    }
    ```

8. 测试代码。 生成项目并启动调试。 应出现实验实例。

9. 打开 **"工具** > **选项"** 页。 您应该在左侧窗格中看到"ToDo"类别。 类别按字母顺序列出，因此请查看 Ts。

10. 在**Todo**选项页上，应看到属性`DaysAhead`设置为**0**。 将其更改为**2**。

11. 在 **"查看/其他窗口"** 菜单上，打开**TodoWindow**。 在文本框中键入**结束日期**，然后单击"**添加**"。

12. 在列表框中，您应该比今天晚两天看到日期。

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>将文本添加到"输出"窗口，并将项添加到任务列表
 对于**任务列表**，您将创建类型 Task 的新对象，然后通过调用其`Add`方法将该任务对象添加到**任务列表中**。 要写入 **"输出"** 窗口，请调用其`GetPane`方法以获取窗格对象，然后调用窗格对象`OutputString`的方法。

1. 在*TodoWindowControl.xaml.cs*中，`button1_Click`在 方法中添加代码以获取**输出**窗口的 **"常规**"窗格（默认值），然后写入它。 方法应如下所示：

    ```csharp
    private void button1_Click(object sender, EventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);

            var outputWindow = parent.GetVsService(
                typeof(SVsOutputWindow)) as IVsOutputWindow;
            IVsOutputWindowPane pane;
            Guid guidGeneralPane = VSConstants.GUID_OutWindowGeneralPane;
            outputWindow.GetPane(ref guidGeneralPane, out pane);
            if (pane != null)
            {
                 pane.OutputString(string.Format(
                    "To Do item created: {0}\r\n",
                 item.ToString()));
        }
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. 要将项添加到任务列表，需要 将 嵌套类添加到 TodoWindowControl 类。 嵌套类需要派生自<xref:Microsoft.VisualStudio.Shell.TaskProvider>。 将以下代码添加到类的`TodoWindowControl`末尾。

    ```csharp
    [Guid("72de1eAD-a00c-4f57-bff7-57edb162d0be")]
    public class TodoWindowTaskProvider : TaskProvider
    {
        public TodoWindowTaskProvider(IServiceProvider sp)
            : base(sp)
        {
        }
    }
    ```

3. 接下来向`TodoTaskProvider``TodoWindowControl`类添加私有引用`CreateProvider()`和 方法。 代码应如下所示：

    ```csharp
    private TodoWindowTaskProvider taskProvider;
    private void CreateProvider()
    {
        if (taskProvider == null)
        {
            taskProvider = new TodoWindowTaskProvider(parent);
            taskProvider.ProviderName = "To Do";
        }
    }
    ```

4. 添加`ClearError()`，这将清除任务列表，并将`ReportError()`条目添加到任务列表，`TodoWindowControl`到类。

    ```csharp
    private void ClearError()
    {
        CreateProvider();
        taskProvider.Tasks.Clear();
    }
    private void ReportError(string p)
    {
        CreateProvider();
        var errorTask = new Task();
        errorTask.CanDelete = false;
        errorTask.Category = TaskCategory.Comments;
        errorTask.Text = p;

        taskProvider.Tasks.Add(errorTask);

        taskProvider.Show();

        var taskList = parent.GetVsService(typeof(SVsTaskList))
            as IVsTaskList2;
        if (taskList == null)
        {
            return;
        }

        var guidProvider = typeof(TodoWindowTaskProvider).GUID;
         taskList.SetActiveProvider(ref guidProvider);
    }
    ```

5. 现在实现该方法`CheckForErrors`，如下所示。

    ```csharp
    public void CheckForErrors()
    {
        foreach (TodoItem item in listBox.Items)
        {
            if (item.DueDate < DateTime.Now)
            {
                ReportError("To Do Item is out of date: "
                    + item.ToString());
            }
        }
    }
    ```

## <a name="try-it-out"></a>试用

1. 生成项目并启动调试。 出现实验实例。

2. 打开**Todo 窗口**（**查看** > **其他窗口** > **todoWindow**）.

3. 在文本框中键入内容，然后单击"**添加**"。

     今天之后的 2 天到期日期将添加到列表框中。 不生成错误，任务**列表**（**查看** > **任务列表**） 应没有条目。

4. 现在将 **"工具** > **选项** > **ToDo"** 页上的设置从**2**改为**0**。

5. 在**TodoWindow**中键入其他内容，然后单击"再次**添加**"。 这触发了错误，并且还会在**任务列表中**输入 。

     添加项目时，初始日期设置为现在加 2 天。

6. 在 **"查看"** 菜单上，单击 **"输出"** 以打开 **"输出"** 窗口。

     请注意，每次添加项目时，任务**列表**窗格中都会显示一条消息。

7. 单击列表框中的项目之一。

     "**属性"** 窗口显示项目的两个属性。

8. 更改其中一个属性，然后按**Enter**。

     项目在列表框中更新。
