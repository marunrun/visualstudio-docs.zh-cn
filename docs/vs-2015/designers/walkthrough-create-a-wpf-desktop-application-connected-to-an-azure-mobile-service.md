---
title: 演练：创建连接到 Azure 移动服务的 WPF 桌面应用程序 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 8d42620f-553b-4b04-a38b-f6b306d73a50
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 624fffb9c86a7ad874f27797dfd5251c8585870f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664026"
---
# <a name="walkthrough-create-a-wpf-desktop-application-connected-to-an-azure-mobile-service"></a>演练：创建连接到 Azure 移动服务的 WPF 桌面应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Presentation Foundation (WPF) 可用于快速创建现代桌面应用程序，该程序使用 Azure 移动服务来存储和提供数据。

## <a name="Requirements"></a> 先决条件
 若要完成本演练，你需要具备以下条件：

- Visual Studio 2015 – 支持 WPF 开发的任何版本。

- 活动的 Microsoft Azure 帐户。

  - 你可以在 [此处](https://azure.microsoft.com/pricing/free-trial/)注册一个免费试用帐户。

  - 你可以激活 [MSDN 订阅者权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。 MSDN 订阅每月会为你提供信用额度，你可以使用信用额度支付 Azure 服务。

## <a name="create-a-project-and-add-references"></a>创建项目并添加引用
 第一步是创建 WPF 项目并添加 NuGet 包，以便你可以连接到 Azure 移动服务。

#### <a name="to-create-the-project"></a>要创建项目

1. 在菜单栏上，依次选择 **“文件”** 、 **“新建”** 、 **“项目”** 。

2. 在“新建项目” 对话框框中，展开“Visual C#” 或“Visual Basic” 节点，再选择“Windows” 节点，然后展开“Windows” 节点并选择“经典桌面” 节点。

3. 在模板列表中，选择“WPF 应用程序” 模板。

4. 在“新建项目” 文本框中，键入 `WPFQuickStart`，然后选择“确定” 按钮。

     创建项目并且已将项目文件添加到“解决方案资源管理器”后，将显示名为 **MainWindow.xaml** 的默认应用程序窗口的设计器。

#### <a name="to-add-a-reference-to-the-windows-azure-mobile-services-sdk"></a>若要添加对 Windows Azure Mobile Services SDK 的引用

1. 在“解决方案资源管理器”中，打开“引用” 节点的快捷菜单，然后选择“管理 NuGet 包”。

2. 在“NuGet 程序包管理器”中，选择“搜索”字段并输入 `mobileservices`。

3. 在左窗格中，选择“WindowsAzure.MobileServices”，然后在右窗格中选择“安装” 按钮。

    > [!NOTE]
    > 如果显示“预览” 对话框，检查建议的更改，然后选择“确定” 按钮。

4. 在“接受许可证” 对话框中，查看许可协议条款，然后通过选择“我接受” 按钮接受这些条款。

     必需的引用将添加到“解决方案资源管理器”。

    > [!NOTE]
    > 如果不同意许可条款，选择“我拒绝” 按钮。 你将无法完成本演练的其余部分。

## <a name="create-the-user-interface"></a>创建用户界面
 下一步是创建应用程序的用户界面。 首先创建一个可重用用户控件，用于显示两个标准的并排窗格布局。 将用户控件添加到应用程序主窗口，并添加控件以输入和显示数据，然后编写一些代码来定义与移动服务的交互。

#### <a name="to-add-a-user-control"></a>要添加用户控件

1. 在“解决方案资源管理器”中，打开“WPFQuickStart” 节点的快捷菜单，然后选择“添加”、“新建文件夹”。

2. 将该文件夹命名为 `Common`注册一个免费试用帐户。

3. 打开“Common” 文件夹的快捷菜单，并选择“添加”、“用户控件”。

4. 在“新建项目” 对话框中，选择“名称”字段并输入 `QuickStartTask`，然后选择“确定” 按钮。

     用户控件将被添加到项目，并且 “QuickStartTask.xaml”文件将在设计器中打开。

5. 在设计器下方窗格中，选择 `<Grid>` 和 `</Grid>` 标记，并用它们替换下面的 XAML 代码：

    ```xaml
    <Grid VerticalAlignment="Top">
            <StackPanel Orientation="Horizontal">
                <Border BorderThickness="0,0,1,0" BorderBrush="DarkGray" Margin="0,10" MinWidth="70">
                    <TextBlock Text="{Binding Number}" FontSize="45" Foreground="DarkGray" Margin="20,0"/>
                </Border>
                <StackPanel>
                    <TextBlock Text="{Binding Title}" Margin="10,10,0,0" FontSize="16" FontWeight="Bold" />
                    <TextBlock Text="{Binding Description}" Margin="10,0,0,0" TextWrapping="Wrap" MaxWidth="500" />
                </StackPanel>
            </StackPanel>
        </Grid>
    ```

     此 XAML 代码将创建具有数字、标题和说明字段占位符的可重用布局。 在运行时可将占位符替换为下图中所示的文本。

     ![QuickStartTask 用户控件](../designers/media/wpfquickstart1.PNG "WPFQuickStart1")

6. 在“解决方案资源管理器”中，展开“QuickStartTask.xaml” 节点，然后打开“QuickStartTask.xaml.cs” 或“QuickStartTask.xaml.vb” 文件。

7. 在代码编辑器中，将 `namespace WPFQuickStart.Common` (C#) 命名空间或 `Public Class QuickStartTask` (VB) 方法替换为以下代码：

    ```csharp
    namespace WPFQuickStart.Common
    {
        /// <summary>
        /// Interaction logic for QuickStartTask.xaml
        /// </summary>
        public partial class QuickStartTask : UserControl
        {
            public QuickStartTask()
            {
                this.InitializeComponent();
                this.DataContext = this;
            }

            public int Number
            {
                get { return (int)GetValue(NumberProperty); }
                set { SetValue(NumberProperty, value); }
            }

            // Using a DependencyProperty as the backing store for Number.  This enables animation, styling, binding, etc...
            public static readonly DependencyProperty NumberProperty =
                DependencyProperty.Register("Number", typeof(int), typeof(QuickStartTask), new PropertyMetadata(0));

            public string Title
            {
                get { return (string)GetValue(TitleProperty); }
                set { SetValue(TitleProperty, value); }
            }

            // Using a DependencyProperty as the backing store for Title.  This enables animation, styling, binding, etc...
            public static readonly DependencyProperty TitleProperty =
                DependencyProperty.Register("Title", typeof(string), typeof(QuickStartTask), new PropertyMetadata(default(string)));

            public string Description
            {
                get { return (string)GetValue(DescriptionProperty); }
                set { SetValue(DescriptionProperty, value); }
            }

            // Using a DependencyProperty as the backing store for Description.  This enables animation, styling, binding, etc...
            public static readonly DependencyProperty DescriptionProperty =
                DependencyProperty.Register("Description", typeof(string), typeof(QuickStartTask), new PropertyMetadata(default(string)));
        }
    }
    ```

    ```vb
    Partial Public Class QuickStartTask
            Inherits UserControl

            Public Sub New()
                Me.InitializeComponent()
                Me.DataContext = Me
            End Sub

            Public Property Number() As Integer
                Get
                    Return CInt(Fix(GetValue(NumberProperty)))
                End Get
                Set(ByVal value As Integer)
                    SetValue(NumberProperty, value)
                End Set
            End Property

            ' Using a DependencyProperty as the backing store for Number.  This enables animation, styling, binding, etc...
            Public Shared ReadOnly NumberProperty As DependencyProperty = DependencyProperty.Register("Number", GetType(Integer), GetType(QuickStartTask), New PropertyMetadata(0))

            Public Property Title() As String
                Get
                    Return CStr(GetValue(TitleProperty))
                End Get
                Set(ByVal value As String)
                    SetValue(TitleProperty, value)
                End Set
            End Property

            ' Using a DependencyProperty as the backing store for Title.  This enables animation, styling, binding, etc...
            Public Shared ReadOnly TitleProperty As DependencyProperty = DependencyProperty.Register("Title", GetType(String), GetType(QuickStartTask), New PropertyMetadata(Nothing))

            Public Property Description() As String
                Get
                    Return CStr(GetValue(DescriptionProperty))
                End Get
                Set(ByVal value As String)
                    SetValue(DescriptionProperty, value)
                End Set
            End Property

            ' Using a DependencyProperty as the backing store for Description.  This enables animation, styling, binding, etc...
            Public Shared ReadOnly DescriptionProperty As DependencyProperty = DependencyProperty.Register("Description", GetType(String), GetType(QuickStartTask), New PropertyMetadata(Nothing))
        End Class
    ```

     此代码使用依赖关系属性设置运行时数字、标题和说明字段的值。

8. 在菜单栏上，依次选择“生成”，“生成 WPFQuickStart” 以生成用户控件。

#### <a name="to-create-and-modify-the-main-window"></a>要创建和修改主窗口

1. 在“解决方案资源管理器”中，打开 “MainWindow.xaml”文件。

2. **重要**。 此步骤仅适用于 C#。 如果使用的是 Visual Basic，请跳到下一步。 在设计器下方窗格中，找到行 `xmlns:local=”clr-namespace:WPFQuickStart”` ，并用它替换下面的 XAML 代码：

    ```xaml
    xmlns:local=”clr-namespace:WPFQuickStart.Common”
    ```

3. 在“新建项目” 窗口中，展开“常用” **Common** 类别节点，然后选择“标题” 属性，再输入 `WPF Todo List` 并按“” 键。

     请注意，XAML 窗口中的“标题” 元素会更改以匹配新值。 可以修改 XAML 窗口或“属性” 窗口中的 XAML 属性且更改会同步。

4. 在 XAML 窗口中，将“高度”元素的值设置为 `768`，并将“宽度”属性的值设置为 `1280`。

     这些元素对应于“高度”和“宽度”属性，它们可在“属性”窗口的“布局”类别中找到。

5. 选择 `<Grid>` 和 `</Grid>` 标记，并用它们替换下面的 XAML 代码：

    ```xaml
    <Grid>

            <Grid Margin="50,50,10,10">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="*" />
                </Grid.ColumnDefinitions>
                <Grid.RowDefinitions>
                    <RowDefinition Height="Auto" />
                    <RowDefinition Height="*" />
                </Grid.RowDefinitions>

                <Grid Grid.Row="0" Grid.ColumnSpan="2" Margin="0,0,0,20">
                    <StackPanel>
                        <TextBlock Foreground="#0094ff" FontFamily="Segoe UI Light" Margin="0,0,0,6">MICROSOFT AZURE MOBILE SERVICES</TextBlock>
                        <TextBlock Foreground="Gray" FontFamily="Segoe UI Light" FontSize="45" ><Run Text="My Todo List"/></TextBlock>
                    </StackPanel>
                </Grid>

                <Grid Grid.Row="1">
                    <StackPanel>

                        <local:QuickStartTask Number="1" Title="Insert a TodoItem" Description="Enter some text below and click Save to insert a new todo item into the list." />

                        <StackPanel Orientation="Horizontal" Margin="72,0,0,0">
                            <TextBox x:Name="TodoInput" Margin="5" MinWidth="300"/>
                            <Button x:Name="ButtonSave" Click="ButtonSave_Click" Content="Save"/>
                        </StackPanel>

                    </StackPanel>
                </Grid>

                <Grid Grid.Row="1" Grid.Column="1">
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto" />
                        <RowDefinition />
                    </Grid.RowDefinitions>
                    <StackPanel>
                        <local:QuickStartTask Number="2" Title="Query and Update Data" Description="Click the Refresh button to load the unfinished TodoItems from the Azure Mobile Service. Select the checkbox to mark a ToDo item as complete and update the list." />
                        <Button Margin="72,0,0,0" Name="ButtonRefresh" Click="ButtonRefresh_Click">Refresh</Button>
                    </StackPanel>

                    <ListView Name="ListItems" Margin="62,10,0,0" Grid.Row="1">
                        <ListView.ItemTemplate>
                            <DataTemplate>
                                <StackPanel Orientation="Horizontal">
                                    <CheckBox Name="CheckBoxComplete" IsChecked="{Binding Complete, Mode=TwoWay}" Checked="CheckBoxComplete_Checked" Content="{Binding Text}" Margin="10,5" VerticalAlignment="Center"/>
                                </StackPanel>
                            </DataTemplate>
                        </ListView.ItemTemplate>
                    </ListView>

                </Grid>

            </Grid>
        </Grid>
    ```

     请注意，所做的更改会反映在设计窗口中。 再次说明，你还可以通过从“工具箱” 窗口添加控件，并设置“属性” 窗口中的属性来定义用户界面。 可以在设计器中完成的任何操作也可以在 XAML 代码中完成，反之亦然。

     此时，你的设计应类似于下图。

     ![设计器中的 Mainwindow.xaml](../designers/media/wpfquickstart2.PNG "WPFQuickStart2")

    > [!NOTE]
    > 在操作后面的几个程序期间，如果“错误列表” 处于打开状态，你可能会看到其中的错误。 别担心；一旦完成剩余程序，这些错误就会消失。

6. 在“解决方案资源管理器”中，展开“MainWindow.xaml” 节点并打开“MainWindow.xaml.cs” 或“MainWindow.xaml.vb” 文件。

7. 在代码编辑器中，将以下 `using` 或 `Imports` 指令添加到文件顶部：

    ```csharp
    using Microsoft.WindowsAzure.MobileServices;
    using Newtonsoft.Json;
    ```

    ```vb
    Imports Microsoft.WindowsAzure.MobileServices
    Imports Newtonsoft.Json
    ```

8. 将 “WPFQuickStart”命名空间 (C#) 或 “类 MainWindow”类 (VB) 中的全部代码替换为以下代码：

    ```csharp
    namespace WPFQuickStart
    {
        /// <summary>
        /// Interaction logic for MainWindow.xaml
        /// </summary>
        public class TodoItem
        {
            public string Id { get; set; }

            [JsonProperty(PropertyName = "text")]
            public string Text { get; set; }

            [JsonProperty(PropertyName = "complete")]
            public bool Complete { get; set; }
        }

        public partial class MainWindow : Window
        {
            private MobileServiceCollection<TodoItem, TodoItem> items;
            private IMobileServiceTable<TodoItem> todoTable = App.MobileService.GetTable<TodoItem>();

            public MainWindow()
            {
                InitializeComponent();
            }

            private async void InsertTodoItem(TodoItem todoItem)
            {
                // This code inserts a new TodoItem into the database. When the operation completes
                // and Mobile Services has assigned an Id, the item is added to the CollectionView
                await todoTable.InsertAsync(todoItem);
                items.Add(todoItem);
            }

            private async void RefreshTodoItems()
            {
                try
                {
                    // This code refreshes the entries in the list view by querying the TodoItem table.
                    // The query excludes completed TodoItems
                    items = await todoTable
                        .Where(todoItem => todoItem.Complete == false)
                        .ToCollectionAsync();
                    ListItems.ItemsSource = items;
                }
                catch (MobileServiceInvalidOperationException e)
                {
                    MessageBox.Show(e.Message, "Error loading items");
                }
            }

            private async void UpdateCheckedTodoItem(TodoItem item)
            {
                // This code takes a freshly completed TodoItem and updates the database. When the MobileService
                // responds, the item is removed from the list
                await todoTable.UpdateAsync(item);
                items.Remove(item);
            }

            private void ButtonRefresh_Click(object sender, RoutedEventArgs e)
            {
                RefreshTodoItems();
            }

            private void ButtonSave_Click(object sender, RoutedEventArgs e)
            {
                var todoItem = new TodoItem { Text = TodoInput.Text };
                InsertTodoItem(todoItem);
                TodoInput.Text = "";
            }

            private void CheckBoxComplete_Checked(object sender, RoutedEventArgs e)
            {
                CheckBox cb = (CheckBox)sender;
                TodoItem item = cb.DataContext as TodoItem;
                UpdateCheckedTodoItem(item);
            }

            protected override void OnActivated(EventArgs e)
            {
                RefreshTodoItems();
            }
        }

    }
    ```

    ```vb
    Public Class TodoItem
        Public Property Id() As String

        <JsonProperty(PropertyName:="text")>
        Public Property Text() As String

        <JsonProperty(PropertyName:="complete")>
        Public Property Complete() As Boolean
    End Class

    Partial Public Class MainWindow
        Inherits Window

        Private items As MobileServiceCollection(Of TodoItem, TodoItem)
        Private todoTable As IMobileServiceTable(Of TodoItem) = Application.MobileService.GetTable(Of TodoItem)()

        Public Sub New()
            InitializeComponent()
        End Sub

        Private Async Sub InsertTodoItem(ByVal todoItem As TodoItem)
            ' This code inserts a new TodoItem into the database. When the operation completes
            ' and Mobile Services has assigned an Id, the item is added to the CollectionView
            Await todoTable.InsertAsync(todoItem)
            items.Add(todoItem)
        End Sub

        Private Async Sub RefreshTodoItems()
            Dim exception As MobileServiceInvalidOperationException = Nothing
            Try
                ' This code refreshes the entries in the list view by querying the TodoItem table.
                ' The query excludes completed TodoItems
                items = Await todoTable.Where(Function(todoItem) todoItem.Complete = False).ToCollectionAsync()
            Catch e As MobileServiceInvalidOperationException
                exception = e
            End Try

            If exception IsNot Nothing Then
                MessageBox.Show(exception.Message, "Error loading items")
            Else
                ListItems.ItemsSource = items
            End If
        End Sub

        Private Async Sub UpdateCheckedTodoItem(ByVal item As TodoItem)
            ' This code takes a freshly completed TodoItem and updates the database. When the MobileService
            ' responds, the item is removed from the list
            Await todoTable.UpdateAsync(item)
            items.Remove(item)
        End Sub

        Private Sub ButtonRefresh_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            RefreshTodoItems()
        End Sub

        Private Sub ButtonSave_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Dim todoItem = New TodoItem With {.Text = TodoInput.Text}
            InsertTodoItem(todoItem)
            TodoInput.Text = ""
        End Sub

        Private Sub CheckBoxComplete_Checked(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Dim cb As CheckBox = DirectCast(sender, CheckBox)
            Dim item As TodoItem = TryCast(cb.DataContext, TodoItem)
            UpdateCheckedTodoItem(item)
        End Sub

        Protected Overrides Sub OnActivated(ByVal e As EventArgs)
            RefreshTodoItems()
        End Sub
    End Class
    ```

     此代码使用异步方法定义移动服务中的用户界面和数据库之间的交互。

## <a name="create-the-azure-mobile-service"></a>创建 Azure 移动服务
 最后一步是在 Microsoft Azure 中创建移动服务，添加表来存储数据，然后从应用程序中引用服务实例。

#### <a name="to-create-a-mobile-service"></a>要创建移动服务

1. 打开 Web 浏览器并登录到你的 Microsoft Azure 门户，然后选择“移动服务” 选项卡。

2. 选择“新建”按钮，然后在弹出对话框中依次选择“计算”、“移动服务”和“创建”。

3. 在“新建移动服务”对话框中，选择“URL”文本框并输入 `wpfquickstart01`。

    > [!NOTE]
    > 你可能需要更改该 URL 的数字部分。 Microsoft Azure 要求每个移动服务的 URL 均唯一。

     这会将服务的 URL 设置为 `https://wpfquickstart01.azure-mobile.net/`。

4. 在“数据库” 列表中，选择一个数据库。 由于它可能是不常使用的应用程序，因此建议选择“创建免费的 20MB SQL 数据库” 选项，或选择已与你的订阅关联的免费数据库。

5. 在“区域” 列表中，选择想要在其中部署移动服务的数据中心，然后选择“下一步” （右箭头）按钮。

    > [!NOTE]
    > 对于此服务，你需使用默认的“后端” 设置 **JavaScript**。

6. 如果要创建新数据库，在“指定数据库设置” 页上的“服务器” 列表中，选择“新建 SQL 数据库服务器”，输入你的 **SQL 登录名** 和 **密码**，然后选择“完成” （复选标记）按钮。

7. 如果你选择了一个现有数据库，在“数据库设置” 页上，输入你的 **登录密码** ，然后选择“完成” （复选标记）按钮。

     创建移动服务的过程将开始。 一旦完成该过程，状态将更改为“就绪” ，然后你可以移动到下一步。

8. 在门户中，选择新创建的移动服务，然后选择“管理密钥” 按钮。

9. 在“管理访问密钥” 对话框中，复制 **应用程序密钥**。

     你将在下一过程中使用它。

#### <a name="to-create-a-table"></a>要创建表

1. 在 Microsoft Azure 门户中，选择你的移动服务名称旁边的向右箭头，再在菜单栏上选择“数据”，然后选择“添加表” 链接。

2. 在“新建项目” 对话框中，在“表名” 文本框中输入 `TodoItem`，然后选择“确定” （复选标记）按钮。

     等待表创建好，然后移至最后的过程。

#### <a name="to-add-a-declaration-for-the-mobile-service"></a>要添加移动服务的声明

1. 返回到 Visual Studio。 在“解决方案资源管理器”，展开“App.xaml” (C#) 或“Application.xaml” (Visual Basic) 节点，然后打开“App.xaml.cs” 或“App.xaml.vb” 文件。

2. 在代码编辑器中，将以下 `using` 或 **Imports** 指令添加到文件顶部：

    ```csharp
    using Microsoft.WindowsAzure.MobileServices;
    ```

    ```vb
    Imports Microsoft.WindowsAzure.MobileServices
    ```

3. 将以下声明添加到类中，将 *YOUR SERVICE_HERE* 替换为你的服务 URL 的名称，并将 *YOUR-KEY-HERE* 替换为你在前面的过程中复制的应用程序密钥：

    ```csharp
    public static MobileServiceClient MobileService = new MobileServiceClient(
                 "https://YOUR-SERVICE-HERE.azure-mobile.net/",
                 "YOUR-KEY-HERE"
             );
    ```

    ```vb
    Public Shared MobileService As New MobileServiceClient("https://YOUR-SERVICE-HERE.azure-mobile.net/", "YOUR-KEY-HERE")
    ```

     此代码允许应用程序访问在 Microsoft Azure 上运行的移动服务。

## <a name="test-the-application"></a>测试应用程序
 就是这样 – 你已创建了访问 Azure 移动服务的 WPF 桌面应用程序。 现在剩下的就是运行该应用程序并观察它的运行。

#### <a name="to-run-the-application"></a>要运行应用程序

1. 在菜单栏上，依次选择“调试”、“启动调试” （或按 F5）。

2. 在“新建项目” 文本框中，输入 `Do something`，然后选择“确定” 按钮。

3. `Do something else`，然后选择“确定” 按钮。

     请注意，已将这两个条目添加到“查询和更新数据” 列表，如下图所示。

     ![Todo 项将添加到列表中。](../designers/media/wpfquickstart3.PNG "WPFQuickStart3")

4. 选中列表中的“Do something else” 条目的复选框。

     这将调用 **UpdateCheckedTodoItem** 方法并从列表和数据库中删除该项。

## <a name="next-steps"></a>后续步骤
 你已完成具有 Azure 后端的 WPF 桌面应用程序的相当简单的示例。 当然，实际的应用程序很可能更为复杂，但应用的都是相同的基本概念。 请参阅 [.NET Framework 中的 WPF](https://msdn.microsoft.com/library/ms754130\(v=vs.100\).aspx)。

 你可以通过添加颜色、形状、图形和甚至动画来使用户界面更有吸引力。 请参阅[在 Visual Studio 和 Blend for Visual Studio 中设计 XAML](../designers/designing-xaml-in-visual-studio.md)。

 你可以连接到现有的 SQL 数据库或其他使用 Azure 移动服务的数据源。 请参阅 [移动服务文档](https://azure.microsoft.com/services/app-service/mobile/)。

## <a name="see-also"></a>请参阅
 [演练：我的第一个 WPF 桌面应用程序](../designers/walkthrough-my-first-wpf-desktop-application2.md) [Windows Presentation Foundation 创建新式桌面应用](../designers/create-modern-desktop-applications-with-windows-presentation-foundation.md)程序
