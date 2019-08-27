---
title: 演练：我第一个 WPF 桌面应用程序 2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 3c460fa9-2ea1-413f-ae54-54a1f2a499d1
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bee99bc546eca3787db1f9cd082359afb6881d10
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63421152"
---
# <a name="walkthrough-my-first-wpf-desktop-application"></a>演练：我第一个 WPF 桌面应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

name ="简介"></a>本演练提供了 Windows Presentation Foundation (WPF) 开发的简介。 将创建包含的元素所共有的大多数 WPF 桌面应用程序的基本应用程序：XAML 标记、 代码隐藏、 应用程序定义、 控件、 布局、 数据绑定和样式。  
  
## <a name="Create_The_Application_Code_Files"></a> 创建应用程序项目  
 在本部分中，你将创建应用程序基础结构，其中包括项目和主窗口或窗体。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
1. 在菜单栏上，依次选择“文件”  、“新建”  、“项目”  。  
  
2. 在“新建项目”  对话框框中，展开“Visual C#”  或“Visual Basic”  节点，再选择“Windows”  节点，然后展开“Windows”  节点并选择“经典桌面”  节点。  
  
3. 在模板列表中，选择“WPF 应用程序”  模板。  
  
4. 在“新建项目”  文本框中，键入 `ExpenseIt`，然后选择“确定”  按钮。  
  
     创建项目并且已将项目文件添加到“解决方案资源管理器”  后，将显示名为 **MainWindow.xaml** 的默认应用程序窗口的设计器。  
  
#### <a name="to-modify-the-main-window"></a>若要修改主窗口  
  
1. 在设计器中，选择“MainWindow.xaml”  选项卡（如果它还不是活动的设计器选项卡）。  
  
2. 如果你正在使用 C#，找到行 `<Window x:Class="ExpenseIt.MainWindow"` 并将其替换为 `<NavigationWindow x:Class="ExpenseIt.MainWindow"`。  
  
     如果你正在使用 Visual Basic，找到行 `<Window x:Class=" MainWindow"` 并将其替换为 `<NavigationWindow x:Class="MainWindow"`。  
  
     请注意，当你将 `<Window` 标记更改为 `<NavigationWindow`时，Intellisense 也会自动将结束标记更改为 `</NavigationWindow>` 。  
  
    > [!NOTE]
    > 如果更改标记后  “错误列表”窗口打开，那么你可能会看到几个错误。 别担心，在下几步中进行的更改将使这些消失。  
  
3. 选择 `<Grid>` 和 `</Grid>` 标记，并将其删除。  
  
     **NavigationWindow** 无法包含其他 UI 元素，如“网格”  。  
  
4. 在“属性”  窗口中，展开“常用”  类别节点，然后选择“标题”  属性，再输入 `ExpenseIt` 并按“Enter”  键。  
  
     请注意，XAML 窗口中的“标题”  元素会更改以匹配新值。 可以修改 XAML 窗口或“属性”  窗口中的 XAML 属性且更改会同步。  
  
5. 在 XAML 窗口中，将“高度”  元素的值设置为 `375`，并将“宽度”  属性的值设置为 `500`。  
  
     这些元素对应于“高度”  和“宽度”  属性，它们可在“属性”  窗口的“布局”  类别中找到。  
  
     你的 **MainWindow.xaml** 文件在 C# 中现应如下所示：  
  
    ```xaml  
    <NavigationWindow x:Class="ExpenseIt.MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
            xmlns:local="clr-namespace:ExpenseIt"  
            mc:Ignorable="d"  
            Title="ExpenseIt" Height="375" Width="500">  
  
    </NavigationWindow>  
    ```  
  
     或在 Visual Basic 中应这样显示：  
  
    ```xaml  
    <NavigationWindow x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
            xmlns:local="clr-namespace:ExpenseIt"  
            mc:Ignorable="d"  
            Title="ExpenseIt" Height="375" Width="500">  
  
    </NavigationWindow>  
    ```  
  
#### <a name="to-modify-the-code-behind-file-c"></a>若要修改代码隐藏文件 (C#)  
  
1. 在“解决方案资源管理器”  中，展开“MainWindow.xaml”  节点并打开“MainWindow.xaml.cs”  文件。  
  
2. 找到行 `public partial class MainWindow : Window` 并将其替换为 `public partial class MainWindow : NavigationWindow`。  
  
     此操作会更改 `MainWindow` 类以派生自 `NavigationWindow`。 在 Visual Basic 中，当你更改 XAML 中的窗口时会自动发生这种情况，因此无需更改任何代码。  
  
## <a name="add_files_to_the_application"></a>将文件添加到应用程序  
 在本部分中，你将向应用程序添加两个页面和一个图像。  
  
#### <a name="to-add-a-home-screen"></a>若要添加主屏幕  
  
1. 在“解决方案资源管理器”  中，打开“ExpenseIt”  节点的快捷菜单，选择“添加”  、“页”  。  
  
2. 在“新建项目”  “添加新项”对话框中，选择  “名称”文本框并输入 `ExpenseItHome`，然后选择“确定”  按钮。  
  
     此页是应用程序启动时显示的第一个窗口。  
  
3. 在设计器中，选择“ExpenseItHome.xaml”  选项卡（如果它还不是活动的设计器选项卡）。  
  
4. 选择 `<Title>` 元素并将标题更改为“ExpenseIt – Home”  。  
  
     你的 **ExpenseItHome.xaml** 文件在 C# 中现应如下所示：  
  
    ```xaml  
    <Page x:Class="ExpenseIt.ExpenseItHome"  
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"   
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"   
          xmlns:local="clr-namespace:ExpenseIt"  
          mc:Ignorable="d"   
          d:DesignHeight="300" d:DesignWidth="300"  
          Title="ExpenseIt - Home">  
  
        <Grid>  
  
        </Grid>  
    </Page>  
    ```  
  
     或在 Visual Basic 中应这样显示：  
  
    ```xaml  
    <Page x:Class="ExpenseItHome"  
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"   
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"   
          xmlns:local="clr-namespace:ExpenseIt"  
          mc:Ignorable="d"   
          d:DesignHeight="300" d:DesignWidth="300"  
          Title="ExpenseIt - Home">  
        <Grid>  
  
        </Grid>  
    </Page>  
    ```  
  
5. 在设计器中，选择“MainWindow.xaml”  选项卡。  
  
6. 查找行 `Title="ExpenseIt" Height="375" Width="500">` 元素并添加 `Source="ExpenseItHome.xaml"` 属性。  
  
     这将 **ExpenseItHome.xaml** 设置为应用程序启动时第一个打开的页。 你的 **MainWindow.xaml** 文件在 C# 中现应如下所示：  
  
    ```xaml  
    <NavigationWindow x:Class="ExpenseIt.MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
            xmlns:local="clr-namespace:ExpenseIt"  
            mc:Ignorable="d"  
            Title="ExpenseIt" Height="375" Width="500" Source="ExpenseItHome.xaml">  
  
    </NavigationWindow>  
    ```  
  
     或在 Visual Basic 中应这样显示：  
  
    ```xaml  
    <NavigationWindow x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
            xmlns:local="clr-namespace:ExpenseIt"  
            mc:Ignorable="d"  
            Title="ExpenseIt" Height="375" Width="500" Source="ExpenseItHome.xaml">  
  
    </NavigationWindow>  
    ```  
  
     正如你先前设置的属性一样，你也可以设置“属性”  窗口的“杂项”  类别中的 `Source` 属性。  
  
#### <a name="to-add-a-details-window"></a>若要添加详细信息窗口  
  
1. 在“解决方案资源管理器”  中，打开“ExpenseIt”  节点的快捷菜单，选择“添加”  、“页”  。  
  
2. 在“新建项目”  “添加新项”对话框中，选择  “名称”文本框并输入 `ExpenseReportPage`，然后选择“确定”  按钮。  
  
     此窗口将显示单个费用报表。  
  
3. 在设计器中，选择“ExpenseReportPage.xaml”  选项卡（如果还不是活动的设计器选项卡）。  
  
4. 选择 `<Title>` 元素并将标题更改为“ExpenseIt – View Expense”  。  
  
     你的 ExpenseReportPage.xaml 文件在 C# 中现应如下所示：  
  
    ```xaml  
    <Page x:Class="ExpenseIt.ExpenseReportPage"  
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"   
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"   
          xmlns:local="clr-namespace:ExpenseIt"  
          mc:Ignorable="d"   
          d:DesignHeight="300" d:DesignWidth="300"  
          Title="ExpenseIt - View Expense">  
  
        <Grid>  
  
        </Grid>  
    </Page>  
    ```  
  
     或在 Visual Basic 中应这样显示：  
  
    ```xaml  
    <Page x:Class="ExpenseReportPage"  
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"   
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"   
          xmlns:local="clr-namespace:ExpenseIt"  
          mc:Ignorable="d"   
          d:DesignHeight="300" d:DesignWidth="300"  
          Title="ExpenseIt - View Expense">  
        <Grid>  
  
        </Grid>  
    </Page>  
    ```  
  
5. 在菜单栏上，依次选择  “调试”和“启动调试”  （或按 F5）以运行应用程序。  
  
     下面的插图显示带导航窗口按钮的应用程序。  
  
     ![ExpenseIt 示例屏幕快照](../designers/media/gettingstartedfigure1.png "GettingStartedFigure1")  
  
6. 关闭应用程序以返回到设计模式。  
  
## <a name="Add_Layout"></a> 创建用户界面  
 布局提供有序方式来放置元素，在调整窗体时还管理这些元素的大小和位置。 在本部分，你将创建三行一列的网格。 你将会添加控件到这两页、添加代码，并且最终定义控件的可重用样式。  
  
#### <a name="to-create-the-layout"></a>若要创建布局  
  
1. 打开“ExpenseItHome.xaml”  ，并选择 `<Grid>` 元素。  
  
2. 在“属性”  窗口中，展开“布局”  类别节点并将“边距”  值设置为 `10`（左边距）、`10`（右边距）、`0`（上边距）和 `10`（下边距）。  
  
     元素 `Margin="10,0,10,10"` 添加到 XAML 中的 `<Grid>` 元素。 再强调一下，你可以直接在 XAML 代码中输入这些值，而不用在“属性”窗口中输入  ，效果都相同。  
  
3. 将下面 XAML 代码添加到 `Grid` 元素以创建行和列定义：  
  
    ```xaml  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition />  
    </Grid.ColumnDefinitions>  
    <Grid.RowDefinitions>  
        <RowDefinition Height="Auto"/>  
        <RowDefinition />  
        <RowDefinition Height="Auto"/>  
    </Grid.RowDefinitions>  
    ```  
  
#### <a name="to-add-controls"></a>若要添加控件  
  
1. 打开 **ExpenseItHome.xaml**。  
  
2. 将以下 XAML 代码刚好添加到 `</Grid>` 标记上方以创建 `Border`、 `ListBox` 和 `Button` 控件。  
  
    ```xaml  
    <!-- People list -->  
      <Border Grid.Column="0" Grid.Row="0" Height="35" Padding="5" Background="#4E87D4">  
          <Label VerticalAlignment="Center" Foreground="White">Names</Label>  
      </Border>  
      <ListBox Name="peopleListBox" Grid.Column="0" Grid.Row="1">  
          <ListBoxItem>Mike</ListBoxItem>  
          <ListBoxItem>Lisa</ListBoxItem>  
          <ListBoxItem>John</ListBoxItem>  
          <ListBoxItem>Mary</ListBoxItem>  
      </ListBox>  
  
      <!-- View report button -->  
      <Button Grid.Column="0" Grid.Row="2" Margin="0,10,0,0" Width="125"  
    Height="25" HorizontalAlignment="Right">View</Button>  
  
    ```  
  
     注意控件会出现在设计窗口中。 你也可以通过将控件从“工具箱”  窗口拖到设计窗口并在“属性”  窗口设置其属性来创建控件。  
  
3. 生成并运行应用程序。 下图显示了此过程中 XAML 创建的控件的运行时外观。  
  
     ![ExpenseIt 示例屏幕快照](../designers/media/gettingstartedfigure2.png "GettingStartedFigure2")  
  
4. 关闭应用程序以返回到设计模式。  
  
#### <a name="to-add-a-background-image"></a>若要添加背景图像  
  
1. 选择以下图像，并将其保存为 `watermark.png`。  
  
     ![演练的水印图像](../designers/media/wpf-watermark.png "WPF_watermark")  
  
    > [!NOTE]
    > 或者可以创建自己的图像并将其保存为 `watermark.png`。  
  
2. 在“解决方案资源管理器”  中，打开“ExpenseIt”  节点的快捷菜单，选择“添加”  、“现有项”  。  
  
3. 在“添加现有项”  对话框中，找到刚添加的“watermark.png”  图像，并选中它，然后选择“添加”  按钮。  
  
    > [!NOTE]
    > 你可能需要展开“文件类型”  列表并选择“图像文件”  。  
  
4. 打开“ExpenseItHome.xaml”  文件并将以下 XAML 代码刚好添加到 `</Grid>` 标记上方以创建背景图像：  
  
    ```xaml  
    <Grid.Background>  
        <ImageBrush ImageSource="watermark.png"/>  
    </Grid.Background>  
  
    ```  
  
#### <a name="to-add-a-title"></a>若要添加标题  
  
1. 打开 **ExpenseItHome.xaml**。  
  
2. 查找行 `<Grid.ColumnDefinitions>` 并将以下内容添加到它的下方：  
  
    ```xaml  
    <ColumnDefinition Width="230" />  
  
    ```  
  
     这将在其他列的左侧另外创建一个列，宽度固定为 230 像素。  
  
3. 查找行 `<Grid.RowDefinitions>` 并将以下内容添加到它的下方：  
  
    ```xaml  
    <RowDefinition />  
  
    ```  
  
     这将在网格顶部添加一行。  
  
4. 将 `Grid.Column` 值设置为 1 以将控件移动到第二列。 将每个 `Grid.Row` 值加 1 以将每个控件下移一行。  
  
    1. 查找行 `<Border Grid.Column="0" Grid.Row="0" Height="35" Padding="5" Background="#4E87D4">`。 将 `Grid.Column="0"` 更改为 `Grid.Column="1"` 并将 `Grid.Row="0"` 更改为 `Grid.Row="1"`。  
  
    2. 查找行 `<ListBox Name="peopleListBox" Grid.Column="0" Grid.Row="1"`。 将 `Grid.Column="0"` 更改为 `Grid.Column="1"` 并将 `Grid.Row="1"` 更改为 `Grid.Row="2"`。  
  
    3. 查找行 `<Button Grid.Column="0" Grid.Row="2" Margin="0,10,0,0" Width="125"`。 将 `Grid.Column="0"` 更改为 `Grid.Column="1"` 并将 `Grid.Row="2"` 更改为 `Grid.Row="3"`。  
  
5. 在 `<Border` 元素之前添加以下 XAML 代码以显示标题：  
  
    ```xaml  
    <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"   
            FontWeight="Bold" FontSize="18" Foreground="#0066cc">  
        View Expense Report  
    </Label>  
  
    ```  
  
     **ExpenseItHome.xaml** 的内容在 C# 中现应如下所示：  
  
    ```xaml  
    <Page x:Class="ExpenseIt.ExpenseItHome"  
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"   
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"   
          xmlns:local="clr-namespace:ExpenseIt"  
          mc:Ignorable="d"   
          d:DesignHeight="300" d:DesignWidth="300"  
          Title="ExpenseIt - Home">  
        <Grid Margin="10,0,10,10">  
            <Grid.ColumnDefinitions>  
                <ColumnDefinition Width="230" />  
                <ColumnDefinition />  
            </Grid.ColumnDefinitions>  
            <Grid.RowDefinitions>  
                <RowDefinition />  
                <RowDefinition Height="Auto"/>  
                <RowDefinition />  
                <RowDefinition Height="Auto"/>  
            </Grid.RowDefinitions>  
            <Border Grid.Column="1" Grid.Row="1" Height="35" Padding="5" Background="#4E87D4">  
                <Label VerticalAlignment="Center" Foreground="White">Names</Label>  
            </Border>  
            <!-- People list -->  
            <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"   
            FontWeight="Bold" FontSize="18" Foreground="#0066cc">  
                View Expense Report  
            </Label>  
            <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2">  
                <ListBoxItem>Mike</ListBoxItem>  
                <ListBoxItem>Lisa</ListBoxItem>  
                <ListBoxItem>John</ListBoxItem>  
                <ListBoxItem>Mary</ListBoxItem>  
            </ListBox>  
  
            <!-- View report button -->  
            <Button Grid.Column="1" Grid.Row="3" Margin="0,10,0,0" Width="125"  
    Height="25" HorizontalAlignment="Right">View</Button>  
            <Grid.Background>  
                <ImageBrush ImageSource="watermark.png"/>  
            </Grid.Background>  
        </Grid>  
    </Page>  
    ```  
  
     或在 Visual Basic 中应这样显示：  
  
    ```xaml  
    <Page x:Class="ExpenseItHome"  
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
          xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"   
          xmlns:d="http://schemas.microsoft.com/expression/blend/2008"   
          xmlns:local="clr-namespace:ExpenseIt"  
          mc:Ignorable="d"   
          d:DesignHeight="300" d:DesignWidth="300"  
          Title="ExpenseIt - Home" >  
        <Grid Margin="10,0,10,10">  
            <Grid.ColumnDefinitions>  
                <ColumnDefinition Width="230" />  
                <ColumnDefinition />  
            </Grid.ColumnDefinitions>  
            <Grid.RowDefinitions>  
                <RowDefinition />  
                <RowDefinition Height="Auto"/>  
                <RowDefinition />  
                <RowDefinition Height="Auto"/>  
            </Grid.RowDefinitions>  
            <Border Grid.Column="1" Grid.Row="1" Height="35" Padding="5" Background="#4E87D4">  
                <Label VerticalAlignment="Center" Foreground="White">Names</Label>  
            </Border>  
            <!-- People list -->  
            <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"   
            FontWeight="Bold" FontSize="18" Foreground="#0066cc">  
                View Expense Report  
            </Label>  
            <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2">  
                <ListBoxItem>Mike</ListBoxItem>  
                <ListBoxItem>Lisa</ListBoxItem>  
                <ListBoxItem>John</ListBoxItem>  
                <ListBoxItem>Mary</ListBoxItem>  
            </ListBox>  
  
            <!-- View report button -->  
            <Button Grid.Column="1" Grid.Row="3" Margin="0,10,0,0" Width="125"  
    Height="25" HorizontalAlignment="Right">View</Button>  
            <Grid.Background>  
                <ImageBrush ImageSource="watermark.png"/>  
            </Grid.Background>  
        </Grid>  
    </Page>  
    ```  
  
6. 如果在此时生成并运行应用程序，其外观应类似于下图：  
  
     ![ExpenseIt 示例屏幕快照](../designers/media/gettingstartedfigure3.png "GettingStartedFigure3")  
  
#### <a name="to-add-code-to-the-button"></a>若要将代码添加到按钮  
  
1. 打开 **ExpenseItHome.xaml**。  
  
2. 选择 `<Button` 元素并将以下 XAML 代码紧跟在 **HorizontalAlignment="Right"** 元素的后面：`Click="Button_Click"`。  
  
     这将为按钮的 `Click` 事件添加一个事件处理程序。 “<按钮”  元素代码现应如下所示：  
  
    ```  
    <!-- View report button -->  
      <Button Grid.Column="1" Grid.Row="3" Margin="0,10,0,0" Width="125"  
    Height="25" HorizontalAlignment="Right" Click="Button_Click">View</Button>  
    ```  
  
3. 打开“ExpenseItHome.xaml.cs”  或  “ExpenseItHome.xaml.vb”文件。  
  
4. 将下面的代码添加到 `ExpenseItHome` 类中:  
  
    ```csharp  
    private void Button_Click(object sender, RoutedEventArgs e)  
    {  
        // View Expense Report  
        ExpenseReportPage expenseReportPage = new ExpenseReportPage();  
        this.NavigationService.Navigate(expenseReportPage);  
  
    }  
    ```  
  
    ```vb  
    Private Sub Button_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)  
        ' View Expense Report  
        Dim expenseReportPage As New ExpenseReportPage()  
    Me.NavigationService.Navigate(expenseReportPage)  
    End Sub  
    ```  
  
     单击该按钮时，此事件处理程序将打开“费用报表”页。  
  
#### <a name="to-create-the-ui-for-the-report-page"></a>若要为报表页创建用户界面  
  
1. 打开 **ExpenseReportPage.xaml**。  
  
     此页面显示“主页”页面上所选人员的费用报表。  
  
2. 将以下 XAML 代码添加到 `<Grid>` 和 `</Grid>` 标记之间：  
  
    ```xaml  
    <Grid.Background>  
        <ImageBrush ImageSource="watermark.png" />  
    </Grid.Background>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition Width="230" />  
        <ColumnDefinition />  
    </Grid.ColumnDefinitions>  
    <Grid.RowDefinitions>  
        <RowDefinition Height="Auto" />  
        <RowDefinition />  
    </Grid.RowDefinitions>  
  
    <Label Grid.Column="1" VerticalAlignment="Center" FontFamily="Trebuchet MS"   
    FontWeight="Bold" FontSize="18" Foreground="#0066cc">  
        Expense Report For:  
    </Label>  
    <Grid Margin="10" Grid.Column="1" Grid.Row="1">  
  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition />  
            <ColumnDefinition />  
        </Grid.ColumnDefinitions>  
        <Grid.RowDefinitions>  
            <RowDefinition Height="Auto" />  
            <RowDefinition Height="Auto" />  
            <RowDefinition />  
        </Grid.RowDefinitions>  
  
        <!-- Name -->  
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" Orientation="Horizontal">  
            <Label Margin="0,0,0,5" FontWeight="Bold">Name:</Label>  
            <Label Margin="0,0,0,5" FontWeight="Bold"></Label>  
        </StackPanel>  
  
        <!-- Department -->  
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="1" Orientation="Horizontal">  
            <Label Margin="0,0,0,5" FontWeight="Bold">Department:</Label>  
            <Label Margin="0,0,0,5" FontWeight="Bold"></Label>  
        </StackPanel>  
  
        <Grid Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="2" VerticalAlignment="Top"   
              HorizontalAlignment="Left">  
            <!-- Expense type and Amount table -->  
            <DataGrid  AutoGenerateColumns="False" RowHeaderWidth="0" >  
                <DataGrid.ColumnHeaderStyle>  
                    <Style TargetType="{x:Type DataGridColumnHeader}">  
                        <Setter Property="Height" Value="35" />  
                        <Setter Property="Padding" Value="5" />  
                        <Setter Property="Background" Value="#4E87D4" />  
                        <Setter Property="Foreground" Value="White" />  
                    </Style>  
                </DataGrid.ColumnHeaderStyle>  
                <DataGrid.Columns>  
                    <DataGridTextColumn Header="ExpenseType" />  
                    <DataGridTextColumn Header="Amount"  />  
                </DataGrid.Columns>  
            </DataGrid>  
        </Grid>  
    </Grid>  
    ```  
  
     此用户界面类似于为主页创建的用户界面，但报表数据在“DataGrid”  控件中显示。  
  
3. 生成并运行应用程序。  
  
4. 选择  “视图”按钮。  
  
     出现费用报告页。  
  
     下图显示“费用报表”页。 注意向后导航按钮已启用。  
  
     ![ExpenseIt 示例屏幕快照](../designers/media/gettingstartedfigure4.png "GettingStartedFigure4")  
  
#### <a name="to-style-controls"></a>若要设置控件样式  
  
1. 打开“App.xaml”  文件 (C#) 或  “Application.xaml”文件 (Visual Basic)。  
  
2. 将以下 XAML 添加到 `<Application.Resources>` 和 `</Application.Resources>` 标记之间：  
  
    ```xaml  
    <!-- Header text style -->  
    <Style x:Key="headerTextStyle">  
        <Setter Property="Label.VerticalAlignment" Value="Center"></Setter>  
        <Setter Property="Label.FontFamily" Value="Trebuchet MS"></Setter>  
        <Setter Property="Label.FontWeight" Value="Bold"></Setter>  
        <Setter Property="Label.FontSize" Value="18"></Setter>  
        <Setter Property="Label.Foreground" Value="#0066cc"></Setter>  
    </Style>  
  
    <!-- Label style -->  
    <Style x:Key="labelStyle" TargetType="{x:Type Label}">  
        <Setter Property="VerticalAlignment" Value="Top" />  
        <Setter Property="HorizontalAlignment" Value="Left" />  
        <Setter Property="FontWeight" Value="Bold" />  
        <Setter Property="Margin" Value="0,0,0,5" />  
    </Style>  
  
    <!-- DataGrid header style -->  
    <Style x:Key="columnHeaderStyle" TargetType="{x:Type DataGridColumnHeader}">  
        <Setter Property="Height" Value="35" />  
        <Setter Property="Padding" Value="5" />  
        <Setter Property="Background" Value="#4E87D4" />  
        <Setter Property="Foreground" Value="White" />  
    </Style>  
  
    <!-- List header style -->  
    <Style x:Key="listHeaderStyle" TargetType="{x:Type Border}">  
        <Setter Property="Height" Value="35" />  
        <Setter Property="Padding" Value="5" />  
        <Setter Property="Background" Value="#4E87D4" />  
    </Style>  
  
    <!-- List header text style -->  
    <Style x:Key="listHeaderTextStyle" TargetType="{x:Type Label}">  
        <Setter Property="Foreground" Value="White" />  
        <Setter Property="VerticalAlignment" Value="Center" />  
        <Setter Property="HorizontalAlignment" Value="Left" />  
    </Style>  
  
    <!-- Button style -->  
    <Style x:Key="buttonStyle" TargetType="{x:Type Button}">  
        <Setter Property="Width" Value="125" />  
        <Setter Property="Height" Value="25" />  
        <Setter Property="Margin" Value="0,10,0,0" />  
        <Setter Property="HorizontalAlignment" Value="Right" />  
    </Style>  
    ```  
  
     此 XAML 将添加以下样式：  
  
    - `headerTextStyle`：设置页标题的格式`Label`。  
  
    - `labelStyle`：若要设置格式`Label`控件。  
  
    - `columnHeaderStyle`：若要设置格式`DataGridColumnHeader`。  
  
    - `listHeaderStyle`：若要设置列表标头的格式`Border`控件。  
  
    - `listHeaderTextStyle`：若要设置格式的列表标头**标签**。  
  
    - `buttonStyle`：若要设置格式`Button`上**ExpenseItHome.xaml**可。  
  
3. 打开 **ExpenseItHome.xaml** ，并使用以下 XAML替换 `<Grid>` 和 `</Grid>` 元素之间的所有内容  
  
    ```xaml  
    <Grid.ColumnDefinitions>  
                <ColumnDefinition Width="230" />  
                <ColumnDefinition />  
            </Grid.ColumnDefinitions>  
  
            <Grid.RowDefinitions>  
                <RowDefinition/>  
                <RowDefinition Height="Auto"/>  
                <RowDefinition />  
                <RowDefinition Height="Auto"/>  
            </Grid.RowDefinitions>  
            <Label Grid.Column="1" Style="{StaticResource headerTextStyle}" >  
                View Expense Report  
            </Label>  
            <!-- People list -->  
                  <Border Grid.Column="1" Grid.Row="1" Style="{StaticResource listHeaderStyle}">  
                <Label Style="{StaticResource listHeaderTextStyle}">Names</Label>  
            </Border>  
            <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2">  
                <ListBoxItem>Mike</ListBoxItem>  
                <ListBoxItem>Lisa</ListBoxItem>  
                <ListBoxItem>John</ListBoxItem>  
                <ListBoxItem>Mary</ListBoxItem>  
            </ListBox>  
  
            <!-- View report button -->  
            <Button Grid.Column="1" Grid.Row="3" Click="Button_Click" Style="{StaticResource buttonStyle}">View</Button>  
            <Grid.Background>  
                <ImageBrush ImageSource="watermark.png"  />  
            </Grid.Background>  
    ```  
  
     应用样式会删除和替换定义每个控件外观的属性（如 `VerticalAlignment` 和 `FontFamily` 。  
  
4. 打开 **ExpenseReportPage.xaml** ，并使用以下 XAML替换 `<Grid>` 和最后一个 `</Grid>` 元素之间的所有内容  
  
    ```xaml  
    <Grid.Background>  
        <ImageBrush ImageSource="watermark.png" />  
    </Grid.Background>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition Width="230" />  
        <ColumnDefinition />  
    </Grid.ColumnDefinitions>  
    <Grid.RowDefinitions>  
        <RowDefinition Height="Auto" />  
        <RowDefinition />  
    </Grid.RowDefinitions>  
    <Label Grid.Column="1" Style="{StaticResource headerTextStyle}">  
        Expense Report For:  
    </Label>  
    <Grid Margin="10" Grid.Column="1" Grid.Row="1">  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition />  
            <ColumnDefinition />  
        </Grid.ColumnDefinitions>  
        <Grid.RowDefinitions>  
            <RowDefinition Height="Auto" />  
            <RowDefinition Height="Auto" />  
            <RowDefinition />  
        </Grid.RowDefinitions>  
  
        <!-- Name -->  
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" Orientation="Horizontal">  
            <Label Style="{StaticResource labelStyle}">Name:</Label>  
            <Label Style="{StaticResource labelStyle}"></Label>  
        </StackPanel>  
  
        <!-- Department -->  
        <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="1"   
    Orientation="Horizontal">  
            <Label Style="{StaticResource labelStyle}">Department:</Label>  
            <Label Style="{StaticResource labelStyle}"></Label>  
        </StackPanel>  
  
        <Grid Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="2" VerticalAlignment="Top"   
              HorizontalAlignment="Left">  
            <!-- Expense type and Amount table -->  
            <DataGrid ColumnHeaderStyle="{StaticResource columnHeaderStyle}"   
                      AutoGenerateColumns="False" RowHeaderWidth="0" >  
                <DataGrid.Columns>  
                    <DataGridTextColumn Header="ExpenseType" />  
                    <DataGridTextColumn Header="Amount"  />  
                </DataGrid.Columns>  
            </DataGrid>  
        </Grid>  
    </Grid>  
  
    ```  
  
     这会将样式添加到 `<Label>` 和 `<Border>` 元素。  
  
## <a name="connecting-to-data"></a>连接到数据  
 在此部分中，你将创建数据提供程序和数据模板，然后连接控件以显示数据。  
  
#### <a name="to-bind-data-to-a-control"></a>若要将数据绑定到控件  
  
1. 打开 **ExpenseItHome.xaml** ，并选择 `<Grid>` 元素。  
  
2. 添加以下 XAML 代码：  
  
    ```xaml  
  
    <Grid.Resources>  
    <!-- Expense Report Data -->  
    <XmlDataProvider x:Key="ExpenseDataSource" XPath="Expenses">  
        <x:XData>  
            <Expenses xmlns="">  
                <Person Name="Mike" Department="Legal">  
                    <Expense ExpenseType="Lunch" ExpenseAmount="50" />  
                    <Expense ExpenseType="Transportation" ExpenseAmount="50" />  
                </Person>  
                <Person Name="Lisa" Department="Marketing">  
                    <Expense ExpenseType="Document printing"  
          ExpenseAmount="50"/>  
                    <Expense ExpenseType="Gift" ExpenseAmount="125" />  
                </Person>  
                <Person Name="John" Department="Engineering">  
                    <Expense ExpenseType="Magazine subscription"   
         ExpenseAmount="50"/>  
                    <Expense ExpenseType="New machine" ExpenseAmount="600" />  
                    <Expense ExpenseType="Software" ExpenseAmount="500" />  
                </Person>  
                <Person Name="Mary" Department="Finance">  
                    <Expense ExpenseType="Dinner" ExpenseAmount="100" />  
                </Person>  
            </Expenses>  
        </x:XData>  
    </XmlDataProvider>  
    </Grid.Resources>  
    ```  
  
     此代码将创建包含每人数据的 `XmlDataProvider` 类。 这通常会作为文件加载，但为简单起见数据以内联方式添加。  
  
3. 在 `<Grid.Resources>` 元素内部，添加以下 XAML 代码：  
  
    ```xaml  
    <!-- Name item template -->  
    <DataTemplate x:Key="nameItemTemplate">  
        <Label Content="{Binding XPath=@Name}"/>  
    </DataTemplate>  
    ```  
  
     这将添加一个在“ListBox”  中定义如何显示数据的 `Data Template`。  
  
4. 将现有 `<ListBox>` 元素替换为以下 XAML。  
  
    ```xaml  
    <ListBox Name="peopleListBox" Grid.Column="1" Grid.Row="2"   
             ItemsSource="{Binding Source={StaticResource ExpenseDataSource}, XPath=Person}"  
             ItemTemplate="{StaticResource nameItemTemplate}">  
    </ListBox>  
    ```  
  
     此代码将 `ItemsSource` 的 `ListBox` 属性绑定到数据源并应用数据模板作为 `ItemTemplate`。  
  
#### <a name="to-connect-data-to-controls"></a>若要将数据连接到控件  
  
1. 打开 **ExpenseReportPage.xaml.vb** 或 **ExpenseReportPage.xaml.cs**。  
  
2. 在 C# 中，将以下构造函数添加到 **ExpenseReportPage** 类，或在 Visual Basic 中使用以下内容替换现有类：  
  
    ```csharp  
    // Custom constructor to pass expense report data  
        public ExpenseReportPage(object data):this()  
        {  
            // Bind to expense report data.  
            this.DataContext = data;  
        }  
    ```  
  
    ```vb  
    Partial Public Class ExpenseReportPage  
    Inherits Page  
    Public Sub New()  
    InitializeComponent()  
    End Sub  
  
    ' Custom constructor to pass expense report data  
    Public Sub New(ByVal data As Object)  
    Me.New()  
    ' Bind to expense report data.  
    Me.DataContext = data  
    End Sub  
  
    End Class  
    ```  
  
     此构造函数将数据对象作为参数。 在这种情况下数据对象将包含所选人员的名字。  
  
3. 打开 **ExpenseItHome.xaml.vb** 或 **ExpenseItHome.xaml.cs**。  
  
4. 将 `Click` 事件处理程序代码替换为以下内容：  
  
    ```csharp  
    private void Button_Click(object sender, RoutedEventArgs e)  
    {  
        // View Expense Report  
        ExpenseReportPage expenseReportPage = new ExpenseReportPage(this.peopleListBox.SelectedItem);  
        this.NavigationService.Navigate(expenseReportPage);  
  
    }  
    ```  
  
    ```vb  
    Private Sub Button_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)  
        ' View Expense Report  
        Dim expenseReportPage As New ExpenseReportPage(Me.peopleListBox.SelectedItem)  
        Me.NavigationService.Navigate(expenseReportPage)  
    End Sub  
    ```  
  
     此代码调用新的构造函数。  
  
#### <a name="to-update-the-ui-with-data-templates"></a>若要使用数据模板更新用户界面  
  
1. 打开 **ExpenseReportPage.xaml**。  
  
2. 使用以下内容替换“姓名”  和“部门”  `<StackPanel` 元素的 XAML 代码：  
  
    ```xaml  
    <!-- Name -->  
    <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" Orientation="Horizontal">  
        <Label Style="{StaticResource labelStyle}">Name:</Label>  
        <Label Style="{StaticResource labelStyle}" Content="{Binding XPath=@Name}"></Label>  
    </StackPanel>  
  
    <!-- Department -->  
    <StackPanel Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="1" Orientation="Horizontal">  
        <Label Style="{StaticResource labelStyle}">Department:</Label>  
        <Label Style="{StaticResource labelStyle}" Content="{Binding XPath=@Department}"></Label>  
    </StackPanel>  
  
    ```  
  
     这会将“标签”  控件绑定到相应数据源属性。  
  
3. 在 `<Grid>` 元素内部添加以下 XAML 代码：  
  
    ```xaml  
    <!--Templates to display expense report data-->  
    <Grid.Resources>  
        <!-- Reason item template -->  
        <DataTemplate x:Key="typeItemTemplate">  
            <Label Content="{Binding XPath=@ExpenseType}"/>  
        </DataTemplate>  
        <!-- Amount item template -->  
        <DataTemplate x:Key="amountItemTemplate">  
            <Label Content="{Binding XPath=@ExpenseAmount}"/>  
        </DataTemplate>  
    </Grid.Resources>  
  
    ```  
  
     这定义如何显示费用报表数据。  
  
4. 将 `<DataGrid>` 元素替换为以下内容：  
  
    ```xaml  
    <!-- Expense type and Amount table -->  
    <DataGrid ItemsSource="{Binding XPath=Expense}" ColumnHeaderStyle="{StaticResource columnHeaderStyle}" AutoGenerateColumns="False" RowHeaderWidth="0" >  
  
        <DataGrid.Columns>  
            <DataGridTextColumn Header="ExpenseType" Binding="{Binding XPath=@ExpenseType}"  />  
            <DataGridTextColumn Header="Amount" Binding="{Binding XPath=@ExpenseAmount}" />  
        </DataGrid.Columns>  
  
    </DataGrid>  
    ```  
  
     这将添加“ItemSource”  并为费用项目定义绑定。  
  
5. 生成并运行应用程序。  
  
6. 选择某个人，然后选择“视图”  按钮。  
  
     下图显示具有所应用的控件、布局、样式、数据绑定和数据模板的 ExpenseIt 应用程序的两个页面。  
  
     ![ExpenseIt 示例屏幕快照](../designers/media/gettingstartedfigure5.png "GettingStartedFigure5")  
  
## <a name="Best_Practices"></a>最佳做法  
 此示例演示了 WPF 的基础知识，因此不遵循应用程序开发的最佳做法。 有关 WPF 和.NET Framework 应用程序开发最佳做法的全面介绍，请参阅以下相应的主题：  
  
- 辅助功能 - [辅助功能最佳做法](https://msdn.microsoft.com/library/aa350483\(v=vs.100\).aspx)  
  
- 安全性 - [Windows Presentation Foundation 安全性](https://msdn.microsoft.com/library/aa970906\(v=vs.100\).aspx)  
  
- 本地化 - [WPF 全球化和本地化概述](https://msdn.microsoft.com/library/ms788718\(v=vs.100\).aspx)  
  
- 性能 - [优化 WPF 应用程序性能](https://msdn.microsoft.com/library/aa970683\(v=vs.100\).aspx)  
  
## <a name="Whats_Next"></a> 下一步  
 通过使用 WPF，你现在可以采用大量技术来创建桌面应用程序。 你现在应该基本了解数据绑定 WPF 应用程序的构建基块。 本主题并不详尽，但希望你现在也能够意识到你可以自己发现本主题尚未介绍的技术。  
  
 有关 WPF 体系结构和编程模型的详细信息，请参阅以下主题：  
  
- [WPF 体系结构](https://msdn.microsoft.com/library/ms750441\(v=vs.100\).aspx)  
  
- [XAML 概述](https://msdn.microsoft.com/library/ms752059\(v=vs.100\).aspx)  
  
- [依赖项属性概述](https://msdn.microsoft.com/library/ms752914\(v=vs.100\).aspx)  
  
- [布局系统](https://msdn.microsoft.com/library/ms745058\(v=vs.100\).aspx)  
  
- [样式和模板](https://msdn.microsoft.com/library/bb613570\(v=vs.100\).aspx)  
  
  有关创建应用程序的详细信息，请参阅以下主题：  
  
- [应用程序开发概述](https://msdn.microsoft.com/library/bb613549\(v=vs.100\).aspx)  
  
- [控件概述](https://msdn.microsoft.com/library/bb613551\(v=vs.100\).aspx)  
  
- [数据绑定概述](https://msdn.microsoft.com/library/ms752347\(v=vs.100\).aspx)  
  
- [WPF 图形、动画和媒体概述](https://msdn.microsoft.com/library/ms742562\(v=vs.100\).aspx)  
  
- [WPF 中的文档](https://msdn.microsoft.com/library/ms748388\(v=vs.100\).aspx)  
  
## <a name="see-also"></a>请参阅  
 [演练：创建一个 WPF 桌面应用程序连接到 Azure 移动服务](../designers/walkthrough-create-a-wpf-desktop-application-connected-to-an-azure-mobile-service.md)   
 [使用 Windows Presentation Foundation 创建新式桌面应用程序](../designers/create-modern-desktop-applications-with-windows-presentation-foundation.md)
