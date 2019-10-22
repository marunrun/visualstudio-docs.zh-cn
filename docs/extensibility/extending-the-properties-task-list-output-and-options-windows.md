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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: eba2e7cbe6957ea786693f86a728ffa6b4aa2cb7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72633204"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>扩展 "属性"、"任务列表"、"输出" 和 "选项" 窗口
你可以在 Visual Studio 中访问任何工具窗口。 本演练演示如何将有关工具窗口的信息集成到新的 "**选项**" 页和 "**属性**" 页上的新设置，以及如何写入**任务列表**和**输出**窗口。

## <a name="prerequisites"></a>Prerequisites
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

1. 使用 VSIX 模板创建名为**TodoList**的项目，并添加一个名为**TodoWindow**的自定义工具窗口项模板。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="set-up-the-tool-window"></a>设置工具窗口
 添加要在其中键入新 ToDo 项的文本框、用于将新项添加到列表的按钮，以及用于显示列表项的列表框。

1. 在*TodoWindow*中，从 UserControl 中删除按钮、TextBox 和 system.windows.controls.stackpanel> 控件。

    > [!NOTE]
    > 这不会删除**button1_Click**事件处理程序，你将在后面的步骤中重复使用它。

2. 从 "**工具箱**" 的 "**所有 WPF 控件**" 部分，将 "**画布**" 控件拖动到网格。

3. 将**文本框**、**按钮**和**列表框**拖动到画布上。 排列元素，使文本框和按钮位于同一级别，列表框将填充其下的剩余窗口，如下图所示。

     ![已完成的工具窗口](../extensibility/media/t5-toolwindow.png "T5-ToolWindow")

4. 在 "XAML" 窗格中，找到按钮，并将其 "内容" 属性设置为 "**添加**"。 通过添加 `Click="button1_Click"` 特性，将按钮事件处理程序重新连接到按钮控件。 画布块应如下所示：

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>自定义构造函数

1. 在*TodoWindowControl.xaml.cs*文件中，添加以下 using 指令：

    ```csharp
    using System;
    ```

2. 添加对 TodoWindow 的公共引用，并让 TodoWindowControl 构造函数采用 TodoWindow 参数。 代码应如下所示：

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. 在*TodoWindow.cs*中，更改 TodoWindowControl 构造函数以包括 TodoWindow 参数。 代码应如下所示：

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>创建选项页
 您可以在 "**选项**" 对话框中提供页面，使用户能够更改工具窗口的设置。 创建选项页需要一个描述选项的类，以及一个*TodoListPackage.cs*或*TodoListPackage*文件中的项。

1. 添加一个名为 `ToolsOptions.cs` 的类。 使 `ToolsOptions` 类继承自 <xref:Microsoft.VisualStudio.Shell.DialogPage>。

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. 添加以下 using 指令：

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. 本演练中的 "选项" 页仅提供一个名为 "DaysAhead" 的选项。 将名为**daysAhead**的私有字段和名为**daysAhead**的属性添加到 `ToolsOptions` 类：

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   现在，你必须使项目知道此选项页。

### <a name="make-the-options-page-available-to-users"></a>使选项页对用户可用

1. 在*TodoWindowPackage.cs*中，将 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 添加到 `TodoWindowPackage` 类：

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. ProvideOptionPage 构造函数的第一个参数是前面创建的类 `ToolsOptions` 的类型。 第二个参数 "ToDo" 是 "**选项**" 对话框中的类别名称。 第三个参数 "General" 是 "**选项**" 对话框中可用的子类别的名称。 接下来的两个参数是字符串的资源 Id;第一个是类别的名称，第二个是子类别的名称。 最终参数确定是否可以使用自动化来访问此页。

     当用户打开 "选项" 页面时，它应类似于下图。

     ![选项页](../extensibility/media/t5optionspage.gif "T5OptionsPage")

     请注意 "**待办事项**" 类别和 **"子类别**"。

## <a name="make-data-available-to-the-properties-window"></a>使数据对属性窗口可用
 可以通过创建一个名为 `TodoItem` 的类来创建待办事项列表信息，该类存储有关 ToDo 列表中各个项的信息。

1. 添加一个名为 `TodoItem.cs` 的类。

     当向用户提供工具窗口时，列表框中的项将由 TodoItems 表示。 当用户在列表框中选择其中一项时，"**属性**" 窗口将显示有关项的信息。

     要使数据在 "**属性**" 窗口中可用，可将数据转换为具有两个特殊属性的公共属性，`Description` 和 `Category`。 `Description` 是显示在 "**属性**" 窗口底部的文本。 `Category` 确定当 "**属性**" 窗口显示在**分类**视图中时，属性应出现的位置。 在下图中，"**属性**" 窗口处于**分类**视图中，" **ToDo 字段**" 类别中的 "**名称**" 属性处于选中状态，而 "**名称**" 属性的说明显示在窗口的底部。

     ![“属性”窗口](../extensibility/media/t5properties.png "T5Properties")

2. 将以下 using 指令添加到*TodoItem.cs*文件。

    ```csharp
    using System.ComponentModel;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. 将 `public` 访问修饰符添加到类声明中。

    ```csharp
    public class TodoItem
    {
    }
    ```

     添加这两个属性，`Name` 和 `DueDate`。 稍后我们将执行 `UpdateList()`，`CheckForErrors()`。

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

4. 添加对用户控件的私有引用。 添加一个构造函数，该构造函数采用用户控件和此 ToDo 项的名称。 若要查找 `daysAhead` 的值，它将获取 "选项" 页属性。

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

5. 由于 `TodoItem` 类的实例将存储在列表框中，并且 ListBox 将调用 `ToString` 函数，因此必须重载 `ToString` 函数。 将以下代码添加到*TodoItem.cs*中的构造函数之后和类的末尾之前。

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. 在*TodoWindowControl.xaml.cs*中，将存根方法添加到 `CheckForError` 和 `UpdateList` 方法的 `TodoWindowControl` 类中。 将其放在文件 System.windows.forms.control.processdialogchar 之后和末尾之前。

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     @No__t_0 方法将调用在父对象中具有相同名称的方法，并且该方法将检查是否发生了任何错误并正确处理它们。 @No__t_0 方法将更新父控件中的 ListBox;此类中的 `Name` 和 `DueDate` 属性发生更改时，将调用方法。 稍后将实现它们。

## <a name="integrate-into-the-properties-window"></a>集成到属性窗口
 现在，编写管理 ListBox 的代码，这些代码将绑定到 "**属性**" 窗口。

 必须更改按钮单击处理程序以读取文本框，创建 TodoItem，并将其添加到 ListBox。

1. 使用创建新 TodoItem 的代码替换现有 `button1_Click` 函数，并将其添加到 ListBox。 它调用 `TrackSelection()`，稍后将定义。

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

2. 在设计视图选择 ListBox 控件。 在 "**属性**" 窗口中，单击 "**事件处理程序**" 按钮，然后找到 " **SelectionChanged** " 事件。 在文本框中填写 " **listBox_SelectionChanged**"。 这会为 SelectionChanged 处理程序添加存根，并将其分配给该事件。

3. 实现 `TrackSelection()` 方法。 由于将需要获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 服务，因此需要使 <xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A> 可由 TodoWindowControl 访问。 将以下方法添加到 `TodoWindow` 类：

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. 将以下 using 指令添加到*TodoWindowControl.xaml.cs*：

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. 填写 SelectionChanged 处理程序，如下所示：

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. 现在，填写 TrackSelection 函数，该函数将提供与 "**属性**" 窗口的集成。 当用户将某项添加到列表框或单击列表框中的项时，将调用此函数。 它将 ListBox 的内容添加到 SelectionContainer，并将 SelectionContainer 传递到 "**属性**" 窗口的 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 事件处理程序。 TrackSelection 服务在用户界面（UI）中跟踪选定对象并显示其属性

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

     现在，你有了一个 "**属性**" 窗口可以使用的类，接下来可以将 "**属性**" 窗口与工具窗口集成。 当用户单击工具窗口中的列表框中的项时，"**属性**" 窗口应进行相应更新。 同样，当用户在 "**属性**" 窗口中更改 ToDo 项时，应更新关联的项。

7. 现在，在*TodoWindowControl.xaml.cs*中添加 UpdateList 函数代码的其余部分。 它应删除并重新添加列表框中修改后的 TodoItem。

    ```csharp
    public void UpdateList(TodoItem item)
    {
        var index = listBox.SelectedIndex;
        listBox.Items.RemoveAt(index);
        listBox.Items.Insert(index, item);
        listBox.SelectedItem = index;
    }
    ```

8. 测试代码。 生成项目并启动调试。 应显示实验实例。

9. 打开 "**工具**"  > **选项**"页。 你应在左窗格中看到 "待办事项" 类别。 类别按字母顺序列出，因此请查看 Ts。

10. 在 " **Todo**选项" 页上，应看到 "`DaysAhead`" 属性设置为**0**。 将其更改为**2**。

11. 在 "**视图"/"其他窗口**" 菜单上，打开 " **TodoWindow**"。 在文本框中键入 "**结束**日期"，然后单击 "**添加**"。

12. 在列表框中，应会看到晚于今天的两天的日期。

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>向 "输出" 窗口中添加文本，并将项添加到任务列表
 对于**任务列表**，你将创建一个类型为 Task 的新对象，然后通过调用其 `Add` 方法将该任务对象添加到**任务列表**中。 若要写入 "**输出**" 窗口，请调用其 `GetPane` 方法来获取窗格对象，然后调用窗格对象的 `OutputString` 方法。

1. 在*TodoWindowControl.xaml.cs*的 `button1_Click` 方法中，添加代码以获取 "**输出**" 窗口（默认值）的 "**常规**" 窗格，并向其写入。 方法应如下所示：

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

2. 若要将项添加到任务列表中，需要将嵌套类添加到 TodoWindowControl 类。 嵌套类需要从 <xref:Microsoft.VisualStudio.Shell.TaskProvider> 派生。 将以下代码添加到 `TodoWindowControl` 类的末尾。

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

3. 接下来，将对 `TodoTaskProvider` 的私有引用和 `CreateProvider()` 方法添加到 `TodoWindowControl` 类中。 代码应如下所示：

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

4. 添加 `ClearError()`，这会清除任务列表，并 `ReportError()`，这会将一个条目添加任务列表到 `TodoWindowControl` 类中。

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

5. 现在实现 `CheckForErrors` 方法，如下所示。

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

1. 生成项目并启动调试。 将显示实验实例。

2. 打开**TodoWindow** （**View**  > **其他 Windows**  > **TodoWindow**）。

3. 在文本框中键入内容，然后单击 "**添加**"。

     将今天的截止日期添加到列表框。 不会生成任何错误，并且**任务列表**（**视图** > **任务列表**）不应包含任何条目。

4. 现在，将 "工具 **"  >  "** **工具**" 中的设置  >  "**ToDo** " 页从**2**改回**0**。

5. 键入**TodoWindow**中的其他内容，然后再次单击 "**添加**"。 这会触发一个错误，还会触发**任务列表**中的一个条目。

     添加项时，初始日期设置为现在加上2天。

6. 在 "**视图**" 菜单上，单击 "**输出**" 打开 "**输出**" 窗口。

     请注意，每次添加项时，"**任务列表**" 窗格中都会显示一条消息。

7. 单击列表框中的某个项。

     "**属性**" 窗口显示项的两个属性。

8. 更改其中一个属性，然后按**enter**。

     项目在列表框中更新。
