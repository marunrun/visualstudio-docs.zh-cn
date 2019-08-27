---
title: 通过 WPF 和 Entity Framework 6 创建简单的数据应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 65929fab-5d78-4e04-af1e-cf4957f230f6
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: decb17be7caa4ea0a300ddb4378ac0ad11520109
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145812"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>使用 WPF 和 Entity Framework 6 创建简单的数据应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何在 Visual Studio 中使用 SQL Server LocalDB，Northwind 数据库、 Entity Framework 6 和 Windows Presentation Foundation 创建一个基本"forms over data"应用程序。 它演示如何执行基本数据绑定的大纲-细节视图，并且也包含自定义"绑定导航器"的"移动上的下一步"按钮，"移动上一个""将移到开头，""移到末尾，""更新"和"删除"。  
  
 本文重点介绍在 Visual Studio 中，使用数据工具并不会尝试解释中任何深度的基础技术。 它假定你已基本熟悉 XAML、 实体框架和 SQL。 此示例中也并不演示 MVVM 体系结构，它是用于 WPF 应用程序的标准。 但是，可以将此代码复制到自己非常稍作修改的 MVVM 应用程序。  
  
## <a name="install-and-connect-to-northwind"></a>安装并连接到 Northwind  
 此示例使用 SQL Server Express LocalDB 和 Northwind 示例数据库。 它应适用于其他 SQL 数据库产品同样如果该产品的 ADO.NET 数据提供程序支持实体框架。  
  
1. 如果你尚未安装 SQL Server 2014 LocalDB Express 32 位从[SQL Server 版本的下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)。  
  
2. 按照此处的说明安装 Northwind 示例数据库：[安装 SQL Server 示例数据库](../data-tools/install-sql-server-sample-databases.md)。  
  
3. [添加新连接](../data-tools/add-new-connections.md)northwind。  
  
## <a name="configure-the-project"></a>配置项目  
  
1. 在 Visual Studio 中，选择**文件&#124;新建项目**，然后创建一个新 C# WPF 应用程序。  
  
2. 接下来，将 NuGet 包添加 Entity Framework 6。 在解决方案资源管理器，选择项目节点。 在主菜单中，选择**项目&#124;管理 NuGet 包...**  
  
     ![管理 NuGet 包的菜单项](../data-tools/media/raddata-vs2015-manage-nuget-packages.png "raddata_vs2015_manage_nuget_packages")  
  
3. 在 NuGet 包管理器中，单击**浏览**链接。 实体框架可能是在列表中的顶层包。 单击**安装**右窗格中，按照提示进行操作。 输出窗口将告诉您何时完成安装。  
  
     ![实体框架 NuGet 包](../data-tools/media/raddata-vs2015-nuget-ef.png "raddata_vs2015_Nuget_EF")  
  
4. 现在我们可以使用 Visual Studio 来创建基于 Northwind 数据库的模型。  
  
## <a name="create-the-model"></a>创建模型  
  
1. 右键单击解决方案资源管理器中的项目节点并选择**添加&#124;新建项**。 在左窗格中，在 C# 节点下，选择**数据**，然后在中间窗格中选择**ADO.NET 实体数据模型**。  
  
    ![实体框架模型新项目项](../data-tools/media/raddata-ef-new-project-item.png "raddata EF 新项目项")  
  
2. 调用该模型`Northwind_model`，然后选择确定。 这将显示**实体数据模型向导**。 选择**EF 设计器从数据库**，然后单击**下一步**。  
  
    ![从数据库的 EF 模型](../data-tools/media/raddata-ef-model-from-database.png "raddata 从数据库的 EF 模型")  
  
3. 在下一个屏幕，然后单击选择 LocalDB Northwind**下一步**。  
  
4. 在向导的下一步页中，我们选择的表、 存储的过程和要包含在实体框架模型中其他数据库对象。 展开树视图中的 dbo 节点并选择客户、 订单和订单详细信息。 保留选中的默认值，然后单击**完成**。  
  
    ![选择模型的数据库对象](../data-tools/media/raddata-choose-ef-objects.png "raddata 选择 EF 对象")  
  
5. 向导将生成表示实体框架模型的 C# 类。 这些是纯旧 C# 类，并且我们将数据绑定到 WPF 用户界面。 .Edmx 文件介绍了关系和其他将类与数据库中的对象相关联的元数据。  .Tt 文件是生成的代码，将操作模型并将更改保存到数据库的 T4 模板。 您可以看到所有这些文件在解决方案资源管理器 Northwind_model 节点下：  
  
    ![解决方案资源管理器 EF 模型文件](../data-tools/media/raddata-solution-explorer-ef-model-files.png "raddata 解决方案资源管理器 EF 模型文件")  
  
    .Edmx 文件的设计器图面，可修改一些属性和关系在模型中。 我们不打算在本演练中使用设计器。  
  
6. 常规用途.tt 文件，并且我们需要调整它们以使用 WPF 数据绑定，这要求 ObservableCollections 之一。  在解决方案资源管理器，展开 Northwind_model 节点，直到找到 Northwind_model.tt。 (请确保**不**中 *。上下文.tt 文件即.edmx 文件的正下方）。  
  
   - 替换的两个匹配项<xref:System.Collections.ICollection>与<xref:System.Collections.ObjectModel.ObservableCollection%601>。  
  
   - 替换为第一个匹配项<xref:System.Collections.Generic.HashSet%601>与<xref:System.Collections.ObjectModel.ObservableCollection%601>在第 51 行。 不替换 HashSet 的第二个匹配项  
  
   - 替换的唯一匹配项<xref:System.Collections.Generic>（在第 334 行） 与<xref:System.Collections.ObjectModel>。  
  
7. 按**Ctrl + Shift + B**以生成项目。 如果生成完成后，在 model 类将显示到数据源向导。  
  
   现在我们已准备好将挂接到此模型添加到 XAML 页，以便我们可以查看、 导航和修改数据。  
  
## <a name="databind-the-model-to-the-xaml-page"></a>数据绑定到 XAML 页面模型  
 可以编写自己的数据绑定代码，但可让 Visual Studio 为您做容易得多。  
  
1. 从主菜单中，选择**项目&#124;添加新数据源**以便启动**数据源配置向导**。 选择**对象**因为我们要绑定到模型类不到数据库：  
  
     ![与对象源的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png "raddata 与对象源的数据源配置向导")  
  
2. 选择客户。  （订单的源将自动从生成中客户的订单导航属性。）  
  
     ![将实体类添加为数据源](../data-tools/media/raddata-add-entity-classes-as-data-sources.png "raddata 添加实体类作为数据源")  
  
3. 单击**完成**  
  
4. 导航到代码视图中的 MainWindow.xaml。 我们要使 XAML 对于此示例的目的非常简单。 主窗口的标题更改为更具描述性和现在为 600 x 800 增加其高度和宽度。 稍后可以随时更改它。 现在将这些包含三行定义添加到主网格中，导航按钮，一个用于客户的详细信息，另一个用于显示其订单的网格的一行：  
  
    ```xaml  
    <Grid.RowDefinitions>  
               <RowDefinition Height="auto"/>  
               <RowDefinition Height="auto"/>  
               <RowDefinition Height="*"/>  
           </Grid.RowDefinitions>  
    ```  
  
5. 现在打开 MainWindow.xaml，以便在设计器中查看。 这将导致数据源窗口显示为工具箱旁边的 Visual Studio 窗口边距中的一个选项。 单击选项卡以打开窗口，或其他按**Shift + Alt + D**或选择**视图&#124;其他 Windows&#124;数据源**。 我们要在自己单独的文本的框中的客户类中显示每个属性。 第一次单击客户组合框中的箭头，然后选择**详细信息**。 以便在设计器知道您希望其进入中间的一行，然后将节点拖到设计图面上的中间部分上。  如果您忘记放置位置，您可以以后手动在 XAML 中指定的一行。 默认情况下，控件垂直放置在网格元素中，但现在您可以排列它们想在窗体上。  例如，可能会将名称文本框中放置在顶部，上面的地址上的有用。 这篇文章的示例应用程序对字段重新排序，并为两列中重新排列它们。  
  
     ![为单个控件的客户数据源绑定](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png "raddata 客户数据源绑定到单个控件")  
  
     在代码视图中，您现在可以看到一个新`Grid`中元素的第 1 行 （中间行） 的父网格。 网格具有的父`DataContext`属性，它引用已添加到 CollectionViewSource`Windows.Resources`元素。 提供该数据上下文，当第一个文本框中，例如，绑定"地址"该名称将映射到`Address`属性在当前`Customer`CollectionViewSource 中的对象。  
  
    ```xaml  
    <Grid DataContext="{StaticResource customerViewSource}">  
    ```  
  
6. 客户窗口的上半部分中可见时，我们想要下半部分查看其底部中的订单。 我们将在单个网格视图控件中显示的订单。 大纲-细节数据绑定按预期方式工作，非常重要，我们将绑定到客户类，不到单独的订单节点中的 Orders 属性。 注意下面的插图 ！ 将客户类的 Orders 属性拖动到窗体的下半部分，以便在设计器将其放入第 2 行：  
  
     ![将订单类所需网格](../data-tools/media/raddata-drag-orders-classes-as-grid.png "raddata 拖动订单类为网格")  
  
7. Visual Studio 已生成连接到模型中的事件的 UI 控件的所有绑定代码。 我们需要执行的操作，请参阅一些数据，只需编写一些代码来填充模型。 第一个让我们导航到 MainWindow.xaml.cs，并将数据成员添加到 MainWindow 类中的数据上下文。 已为我们生成，此对象的作用类似于跟踪的更改，并在模型中的事件的控件的内容。 虽然我们在这里，我们将添加两个成员，我们将使用更高版本中添加新客户或新订单。 我们还将添加构造函数初始化逻辑。 我们的类的顶部应如下所示：  
  
    ```csharp  
    public partial class MainWindow : Window  
       {  
           public Customer newCustomer { get; set; }  
           public Order newOrder { get; set; }  
  
           NorthwindEntities context = new NorthwindEntities();  
           CollectionViewSource custViewSource;  
           CollectionViewSource ordViewSource;  
  
           public MainWindow()  
           {  
               InitializeComponent();  
               newCustomer = new Customer();  
               newOrder = new Order();  
               custViewSource = ((CollectionViewSource)  
                   (FindResource("customerViewSource")));  
               ordViewSource = ((CollectionViewSource)  
                   (FindResource("customerOrdersViewSource")));  
               DataContext = this;  
           }  
    ```  
  
     添加`using`指令 System.Data.Entity 将 Load 扩展方法引入作用域：  
  
    ```csharp  
    using System.Data.Entity;  
    ```  
  
     现在向下滚动并找到 Window_Loaded 事件处理程序。 请注意我们 Visual Studio 添加了 CollectionViewSource 对象。 这表示我们在创建模型时所选择的 NorthwindEntities 对象。 让我们将代码添加到 Window_loaded，以便整个方法现在如下所示：  
  
    ```csharp  
    private void Window_Loaded(object sender, RoutedEventArgs e)  
        {  
            // Load is an extension method on IQueryable,    
            // defined in the System.Data.Entity namespace.   
            // This method enumerates the results of the query,    
            // similar to ToList but without creating a list.   
            // When used with Linq to Entities this method    
            // creates entity objects and adds them to the context.   
            context.Customers.Load();  
  
            // After the data is loaded call the DbSet<T>.Local property    
            // to use the DbSet<T> as a binding source.   
            custViewSource.Source = context.Customers.Local;  
        }  
    ```  
  
8. 按 F5  。 你应看到已检索到 CollectionViewSource，及其在数据网格中的订单的第一个客户的详细信息。 格式设置不是太好了，因此让我们来修复的。 创建一种方法，若要查看其他记录，并执行基本的 CRUD 操作。  
  
## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>调整页面设计并添加新客户和订单的网格  
 Visual Studio 生成的默认排列方式是不适合我们的应用程序，因此我们将在 XAML 中手动进行一些更改。 我们还将需要一些"forms"（这是实际网格），使用户能够添加新客户或新订单。    为了能够添加新客户和订单，我们需要一组单独的不是数据绑定到的文本框`CollectionViewSource`。 我们将控制哪些用户会看到在任何给定时间通过将 Visible 属性设置的处理程序方法中的网格。  
  
 最后，我们将添加到订单网格以使用户能够删除各个订单中的每一行的删除按钮。  
  
 首先，将这些样式添加到 Windows.Resources:  
  
```xaml  
<Style x:Key="Label" TargetType="{x:Type Label}" BasedOn="{x:Null}">  
    <Setter Property="HorizontalAlignment" Value="Left"/>  
    <Setter Property="VerticalAlignment" Value="Center"/>  
    <Setter Property="Margin" Value="3"/>  
    <Setter Property="Height" Value="23"/>  
</Style>  
<Style x:Key="CustTextBox" TargetType="{x:Type TextBox}" BasedOn="{x:Null}">  
    <Setter Property="HorizontalAlignment" Value="Right"/>  
    <Setter Property="VerticalAlignment" Value="Center"/>  
    <Setter Property="Margin" Value="3"/>  
    <Setter Property="Height" Value="26"/>  
    <Setter Property="Width" Value="120"/>  
</Style>  
```  
  
 接下来，使用此标记替换整个外部网格：  
  
```xaml  
<Grid >  
     <Grid.RowDefinitions>  
         <RowDefinition Height="auto"/>  
         <RowDefinition Height="auto"/>  
         <RowDefinition Height="*"/>  
     </Grid.RowDefinitions>  
     <StackPanel  Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">  
         <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"  />  
         <Button Name="btnPrev"  Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>  
         <Button Name="btnNext"  Content="►" Command="{StaticResource NextCommand}"     Style="{StaticResource NavButton}"/>  
         <Button Name="btnLast"  Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>  
         <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>  
         <Button  Name="btnAdd"   Content="New Customer"  Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>  
         <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>  
         <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>  
         <Button Content="Cancel" Name="btnCancel"  Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>  
     </StackPanel>  
     <Grid x:Name="existingCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" Margin="5" Visibility="Visible" VerticalAlignment="Top" Background="AntiqueWhite" DataContext="{StaticResource customerViewSource}">  
         <Grid.ColumnDefinitions>  
             <ColumnDefinition Width="Auto" MinWidth="233"/>  
             <ColumnDefinition Width="Auto" MinWidth="397"/>  
         </Grid.ColumnDefinitions>  
         <Grid.RowDefinitions>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
         </Grid.RowDefinitions>  
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>  
         <TextBox x:Name="customerIDTextBox"  Grid.Row="0" Style="{StaticResource CustTextBox}"   
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Company Name:"  Grid.Row="1" Style="{StaticResource Label}"/>  
         <TextBox x:Name="companyNameTextBox"  Grid.Row="1" Style="{StaticResource CustTextBox}"   
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Contact Name:"  Grid.Row="2" Style="{StaticResource Label}"/>  
         <TextBox x:Name="contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"   
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Contact Title:"  Grid.Row="3" Style="{StaticResource Label}"/>  
         <TextBox x:Name="contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"   
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>  
         <TextBox x:Name="addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="City:" Grid.Column="1" Grid.Row="0"  Style="{StaticResource Label}"/>  
         <TextBox x:Name="cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"   
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>  
         <TextBox x:Name="countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>  
         <TextBox x:Name="faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>  
         <TextBox x:Name="phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>  
         <TextBox x:Name="postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"   
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>  
         <TextBox x:Name="regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
     </Grid>  
     <Grid x:Name="newCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type Window}}, Path=newCustomer, UpdateSourceTrigger=Explicit}" Visibility="Collapsed" Background="CornflowerBlue">  
         <Grid.ColumnDefinitions>  
             <ColumnDefinition Width="Auto" MinWidth="233"/>  
             <ColumnDefinition Width="Auto" MinWidth="397"/>  
         </Grid.ColumnDefinitions>  
         <Grid.RowDefinitions>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
         </Grid.RowDefinitions>  
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_customerIDTextBox"  Grid.Row="0"  Style="{StaticResource CustTextBox}"   
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Company Name:"  Grid.Row="1" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_companyNameTextBox"  Grid.Row="1" Style="{StaticResource CustTextBox}"   
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true }"/>  
         <Label Content="Contact Name:"  Grid.Row="2" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"   
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Contact Title:"  Grid.Row="3" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"   
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="City:" Grid.Column="1" Grid.Row="0"  Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"   
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"   
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
     </Grid>  
     <Grid x:Name="newOrderGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding Path=newOrder, Mode=TwoWay}" Visibility="Collapsed" Background="LightGreen">  
         <Grid.ColumnDefinitions>  
             <ColumnDefinition Width="Auto" MinWidth="233"/>  
             <ColumnDefinition Width="Auto" MinWidth="397"/>  
         </Grid.ColumnDefinitions>  
         <Grid.RowDefinitions>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
             <RowDefinition Height="Auto"/>  
         </Grid.RowDefinitions>  
         <Label Content="New Order Form" FontWeight="Bold"/>  
         <Label Content="Employee ID:"  Grid.Row="1" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_employeeIDTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"   
                  Text="{Binding EmployeeID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Order Date:"  Grid.Row="2" Style="{StaticResource Label}"/>  
         <DatePicker x:Name="add_orderDatePicker" Grid.Row="2"  HorizontalAlignment="Right" Width="120"  
                 SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>  
         <Label Content="Required Date:" Grid.Row="3" Style="{StaticResource Label}"/>  
         <DatePicker x:Name="add_requiredDatePicker" Grid.Row="3" HorizontalAlignment="Right" Width="120"  
                  SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>  
         <Label Content="Shipped Date:"  Grid.Row="4"  Style="{StaticResource Label}"/>  
         <DatePicker x:Name="add_shippedDatePicker"  Grid.Row="4"  HorizontalAlignment="Right" Width="120"  
                 SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>  
         <Label Content="Ship Via:"  Grid.Row="5" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_ShipViaTextBox"  Grid.Row="5" Style="{StaticResource CustTextBox}"   
                  Text="{Binding ShipVia, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
         <Label Content="Freight"  Grid.Row="6" Style="{StaticResource Label}"/>  
         <TextBox x:Name="add_freightTextBox" Grid.Row="6" Style="{StaticResource CustTextBox}"   
                  Text="{Binding Freight, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>  
     </Grid>  
     <DataGrid x:Name="ordersDataGrid" SelectionUnit="Cell" SelectionMode="Single" AutoGenerateColumns="False" CanUserAddRows="false" IsEnabled="True" EnableRowVirtualization="True" Width="auto" ItemsSource="{Binding Source={StaticResource customerOrdersViewSource}}" Margin="10,10,10,10" Grid.Row="2" RowDetailsVisibilityMode="VisibleWhenSelected">  
         <DataGrid.Columns>  
             <DataGridTemplateColumn>  
                 <DataGridTemplateColumn.CellTemplate>  
                     <DataTemplate>  
                         <Button Content="Delete"  Command="{StaticResource DeleteOrderCommand}" CommandParameter="{Binding}"/>  
                     </DataTemplate>  
                 </DataGridTemplateColumn.CellTemplate>  
             </DataGridTemplateColumn>  
             <DataGridTextColumn x:Name="customerIDColumn" Binding="{Binding CustomerID}" Header="Customer ID" Width="SizeToHeader"/>  
             <DataGridTextColumn x:Name="employeeIDColumn" Binding="{Binding EmployeeID}" Header="Employee ID" Width="SizeToHeader"/>  
             <DataGridTextColumn x:Name="freightColumn" Binding="{Binding Freight}" Header="Freight" Width="SizeToHeader"/>  
             <DataGridTemplateColumn x:Name="orderDateColumn" Header="Order Date" Width="SizeToHeader">  
                 <DataGridTemplateColumn.CellTemplate>  
                     <DataTemplate>  
                         <DatePicker SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>  
                     </DataTemplate>  
                 </DataGridTemplateColumn.CellTemplate>  
             </DataGridTemplateColumn>  
             <DataGridTextColumn x:Name="orderIDColumn" Binding="{Binding OrderID}" Header="Order ID" Width="SizeToHeader"/>  
             <DataGridTemplateColumn x:Name="requiredDateColumn" Header="Required Date" Width="SizeToHeader">  
                 <DataGridTemplateColumn.CellTemplate>  
                     <DataTemplate>  
                         <DatePicker SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>  
                     </DataTemplate>  
                 </DataGridTemplateColumn.CellTemplate>  
             </DataGridTemplateColumn>  
             <DataGridTextColumn x:Name="shipAddressColumn" Binding="{Binding ShipAddress}" Header="Ship Address" Width="SizeToHeader"/>  
             <DataGridTextColumn x:Name="shipCityColumn" Binding="{Binding ShipCity}" Header="Ship City" Width="SizeToHeader"/>  
             <DataGridTextColumn x:Name="shipCountryColumn" Binding="{Binding ShipCountry}" Header="Ship Country" Width="SizeToHeader"/>  
             <DataGridTextColumn x:Name="shipNameColumn" Binding="{Binding ShipName}" Header="Ship Name" Width="SizeToHeader"/>  
             <DataGridTemplateColumn x:Name="shippedDateColumn" Header="Shipped Date" Width="SizeToHeader">  
                 <DataGridTemplateColumn.CellTemplate>  
                     <DataTemplate>  
                         <DatePicker SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>  
                     </DataTemplate>  
                 </DataGridTemplateColumn.CellTemplate>  
             </DataGridTemplateColumn>  
             <DataGridTextColumn x:Name="shipPostalCodeColumn" Binding="{Binding ShipPostalCode}" Header="Ship Postal Code" Width="SizeToHeader"/>  
             <DataGridTextColumn x:Name="shipRegionColumn" Binding="{Binding ShipRegion}" Header="Ship Region" Width="SizeToHeader"/>  
             <DataGridTextColumn x:Name="shipViaColumn" Binding="{Binding ShipVia}" Header="Ship Via" Width="SizeToHeader"/>  
         </DataGrid.Columns>  
     </DataGrid>  
 </Grid>  
```  
  
## <a name="add-buttons-to-navigate-add-update-and-delete"></a>添加按钮，以导航、 添加、 更新和删除  
 在 Windows 窗体应用程序中的数据库中的行中导航并执行基本的 CRUD 操作获取具有按钮的 BindingNavigator 对象。 WPF 不提供 BindingNavigator，但它们是轻松地进行。 我们将使用按钮在页网格中的底部行中水平 StackPanel 那样做，我们会将这些按钮与绑定到方法后面的代码中的命令相关联。  
  
 有个 4 命令逻辑部分：（1） 命令、 （2） 绑定、 （3) 按钮和隐藏代码中 （4） 的命令处理程序。  
  
#### <a name="add-commands-bindings-and-buttons-in-xaml"></a>在 XAML 中添加命令、 绑定和按钮  
  
1. 首先，让我们在我们 Windows.Resources 元素内的 MainWindow.XAML 文件中添加的命令：  
  
    ```xaml  
  
     <RoutedUICommand x:Key="FirstCommand" Text="First"/>  
    <RoutedUICommand x:Key="LastCommand" Text="Last"/>  
    <RoutedUICommand x:Key="NextCommand" Text="Next"/>  
    <RoutedUICommand x:Key="PreviousCommand" Text="Previous"/>  
    <RoutedUICommand x:Key="DeleteCustomerCommand" Text="Delete Customer"/>  
    <RoutedUICommand x:Key="DeleteOrderCommand" Text="Delete Order"/>  
    <RoutedUICommand x:Key="UpdateCommand" Text="Update"/>  
    <RoutedUICommand x:Key="AddCommand" Text="Add"/>  
    <RoutedUICommand x:Key="CancelCommand" Text="Cancel"/>  
    ```  
  
2. CommandBinding 将 RoutedUICommand 事件映射到代码隐藏中的方法。 结束标记 Windows.Resources 后添加此 CommandBindings 元素：  
  
    ```xaml  
  
        <Window.CommandBindings>  
        <CommandBinding Command="{StaticResource FirstCommand}" Executed="FirstCommandHandler"/>  
        <CommandBinding Command="{StaticResource LastCommand}" Executed="LastCommandHandler"/>  
        <CommandBinding Command="{StaticResource NextCommand}" Executed="NextCommandHandler"/>  
        <CommandBinding Command="{StaticResource PreviousCommand}" Executed="PreviousCommandHandler"/>  
        <CommandBinding Command="{StaticResource DeleteCustomerCommand}" Executed="DeleteCustomerCommandHandler"/>  
        <CommandBinding Command="{StaticResource DeleteOrderCommand}" Executed="DeleteOrderCommandHandler"/>  
        <CommandBinding Command="{StaticResource UpdateCommand}" Executed="UpdateCommandHandler"/>  
        <CommandBinding Command="{StaticResource AddCommand}" Executed="AddCommandHandler"/>  
        <CommandBinding Command="{StaticResource CancelCommand}" Executed="CancelCommandHandler"/>  
    </Window.CommandBindings>  
    ```  
  
3. 现在让我们添加导航条 StackPanel、 添加、 删除和更新按钮。 首先，将此样式添加到 Windows.Resources:  
  
    ```xaml  
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">  
        <Setter Property="FontSize" Value="24"/>  
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>  
        <Setter Property="Margin" Value="2,2,2,0"/>  
        <Setter Property="Width" Value="40"/>  
        <Setter Property="Height" Value="auto"/>  
    </Style>  
    ```  
  
     现在只需在 XAML 页面的顶部附近的外部网格元素 RowDefinitions 后粘贴此代码：  
  
    ```xaml  
    <StackPanel  Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">  
        <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"  />  
        <Button Name="btnPrev"  Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>  
        <Button Name="btnNext"  Content="►" Command="{StaticResource NextCommand}"     Style="{StaticResource NavButton}"/>  
        <Button Name="btnLast"  Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>  
        <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>  
        <Button  Name="btnAdd"   Content="New Customer"  Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>  
        <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>  
        <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>  
        <Button Content="Cancel" Name="btnCancel"  Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>  
    </StackPanel>  
    ```  
  
#### <a name="add-command-handlers-to-the-mainwindow-class"></a>向 MainWindow 类中添加命令处理程序  
  
1. 代码隐藏很小的添加和删除方法除外。 请注意，通过 CollectionViewSource 视图属性上调用方法来执行导航。 DeleteOrderCommandHandler 演示如何在订单执行级联删除。 我们必须先删除与之关联 Order_Details。 UpdateCommandHandler 将新客户添加到集合中，否则只需使用任何内容更改用户所做的文本框中更新现有对象。  
  
2. 将这些处理程序方法添加到 MainWindow 类在 MainWindow.xaml.cs 中，如果你 CollectionViewSource 为 Customers 表具有不同的名称，然后你将需要调整中的每个这些方法的名称：  
  
    ```csharp  
       private void LastCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        custViewSource.View.MoveCurrentToLast();  
    }  
  
    private void PreviousCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        custViewSource.View.MoveCurrentToPrevious();  
    }  
  
    private void NextCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        custViewSource.View.MoveCurrentToNext();  
    }  
  
    private void FirstCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        custViewSource.View.MoveCurrentToFirst();  
    }  
  
    private void DeleteCustomerCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        // If existing window is visible, then delete the customer and all their orders.  
        // In a real application, you should add warnings and allow a user to cancel the operation.  
        var cur = custViewSource.View.CurrentItem as Customer;  
  
        var cust = (from c in context.Customers  
                    where c.CustomerID == cur.CustomerID  
                    select c).FirstOrDefault();  
  
        if (cust != null)  
        {  
            foreach (var ord in cust.Orders.ToList())  
            {  
                Delete_Order(ord);  
            }  
            context.Customers.Remove(cust);  
        }  
        context.SaveChanges();  
        custViewSource.View.Refresh();  
    }  
  
    // Commit changes from the new customer form, the new order form,  
    // or edits made to the existing customer form.  
    private void UpdateCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        if (newCustomerGrid.IsVisible)  
        {  
            // Create a new object because the old one  
            // is being tracked by EF now.  
            newCustomer = new Customer();   
            newCustomer.Address = add_addressTextBox.Text;  
            newCustomer.City = add_cityTextBox.Text;  
            newCustomer.CompanyName = add_companyNameTextBox.Text;  
            newCustomer.ContactName = add_contactNameTextBox.Text;  
            newCustomer.ContactTitle = add_contactTitleTextBox.Text;  
            newCustomer.Country = add_countryTextBox.Text;  
            newCustomer.CustomerID = add_customerIDTextBox.Text;  
            newCustomer.Fax = add_faxTextBox.Text;  
            newCustomer.Phone = add_phoneTextBox.Text;  
            newCustomer.PostalCode = add_postalCodeTextBox.Text;  
            newCustomer.Region = add_regionTextBox.Text;  
  
            // Perform very basic validation  
            if (newCustomer.CustomerID.Length == 5)  
            {  
                // Insert the new customer at correct position:  
                int len = context.Customers.Local.Count();  
                int pos = len;  
                for (int i = 0; i < len; ++i)  
                {  
                    if (String.CompareOrdinal(newCustomer.CustomerID, context.Customers.Local[i].CustomerID) < 0)  
                    {  
                        pos = i;  
                        break;  
                    }  
                }  
                context.Customers.Local.Insert(pos, newCustomer);  
                custViewSource.View.Refresh();  
                custViewSource.View.MoveCurrentTo(newCustomer);  
            }  
            else  
            {  
                MessageBox.Show("CustomerID must have 5 characters.");  
            }  
  
            newCustomerGrid.Visibility = Visibility.Collapsed;  
            existingCustomerGrid.Visibility = Visibility.Visible;  
        }  
        else if (newOrderGrid.IsVisible)  
        {  
            // Order ID is auto-generated so we don't set it here.  
            // For CustomerID, address, etc we use the values from current customer.  
            // User can modify these in the datagrid after the order is entered.  
  
            newOrder.OrderDate = add_orderDatePicker.SelectedDate;  
            newOrder.RequiredDate = add_requiredDatePicker.SelectedDate;  
            newOrder.ShippedDate = add_shippedDatePicker.SelectedDate;  
            try  
            {  
                // Exercise for the reader if you are using Northwind:  
                // Add the Northwind Shippers table to the model.  
                // Acceptable ShipperID values are 1, 2, or 3.  
                if (add_ShipViaTextBox.Text == "1" || add_ShipViaTextBox.Text == "2"  
                    || add_ShipViaTextBox.Text == "3")  
                {  
                    newOrder.ShipVia = Convert.ToInt32(add_ShipViaTextBox.Text);  
                }  
                else  
                {  
                    MessageBox.Show("Shipper ID must be 1, 2, or 3 in Northwind.");  
                    return;  
                }  
            }  
            catch  
            {  
                MessageBox.Show("Ship Via must be convertible to int");  
                return;  
            }  
            try  
            {  
                newOrder.Freight = Convert.ToDecimal(add_freightTextBox.Text);  
            }  
            catch  
            {  
                MessageBox.Show("Freight must be convertible to decimal.");  
                return;  
            }  
  
            // Add the order into the EF model  
            context.Orders.Add(newOrder);  
            ordViewSource.View.Refresh();  
        }  
  
        // Save the changes, either for a new customer, a new order  
        // or an edit in an existing customer or order  
        context.SaveChanges();  
    }  
  
    // Sets up the form so that user can enter data. Data is later  
    // saved when user clicks Commit.  
    private void AddCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        existingCustomerGrid.Visibility = Visibility.Collapsed;  
        newOrderGrid.Visibility = Visibility.Collapsed;  
        newCustomerGrid.Visibility = Visibility.Visible;  
  
        // Clear all the text boxes before adding a new customer.  
        foreach (var child in newCustomerGrid.Children)  
        {  
            var tb = child as TextBox;  
            if (tb != null)  
            {  
                tb.Text = "";  
            }  
        }  
    }  
  
    private void NewOrder_click(object sender, RoutedEventArgs e)  
    {  
        var cust = custViewSource.View.CurrentItem as Customer;  
        if (cust == null)  
        {  
            MessageBox.Show("No customer selected.");  
            return;  
        }  
  
        newOrder.CustomerID = cust.CustomerID;  
  
        // Get address and other mostly constant fields from   
        // an existing order, if one exists  
        var coll = custViewSource.Source as IEnumerable<Customer>;  
        var lastOrder = (from c in coll  
                         from ord in c.Orders  
                         select ord).LastOrDefault();  
        if (lastOrder != null)  
        {  
            newOrder.ShipAddress = lastOrder.ShipAddress;  
            newOrder.ShipCity = lastOrder.ShipCity;  
            newOrder.ShipCountry = lastOrder.ShipCountry;  
            newOrder.ShipName = lastOrder.ShipName;  
            newOrder.ShipPostalCode = lastOrder.ShipPostalCode;  
            newOrder.ShipRegion = lastOrder.ShipRegion;  
        }  
  
        existingCustomerGrid.Visibility = Visibility.Collapsed;  
        newCustomerGrid.Visibility = Visibility.Collapsed;  
        newOrderGrid.UpdateLayout();  
        newOrderGrid.Visibility = Visibility.Visible;  
    }  
  
    // Cancels any input into the new customer form  
    private void CancelCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        add_addressTextBox.Text = "";  
        add_cityTextBox.Text = "";  
        add_companyNameTextBox.Text = "";  
        add_contactNameTextBox.Text = "";  
        add_contactTitleTextBox.Text = "";  
        add_countryTextBox.Text = "";  
        add_customerIDTextBox.Text = "";  
        add_faxTextBox.Text = "";  
        add_phoneTextBox.Text = "";  
        add_postalCodeTextBox.Text = "";  
        add_regionTextBox.Text = "";  
  
        existingCustomerGrid.Visibility = Visibility.Visible;  
        newCustomerGrid.Visibility = Visibility.Collapsed;  
        newOrderGrid.Visibility = Visibility.Collapsed;  
    }  
  
    private void Delete_Order(Order order)  
    {  
        // Find the order in the EF model.  
        var ord = (from o in context.Orders.Local  
                   where o.OrderID == order.OrderID  
                   select o).FirstOrDefault();  
  
        // Delete all the order_details that have  
        // this Order as a foreign key  
        foreach (var detail in ord.Order_Details.ToList())  
        {  
            context.Order_Details.Remove(detail);  
        }  
  
        // Now it's safe to delete the order.  
        context.Orders.Remove(ord);  
        context.SaveChanges();  
  
        // Update the data grid.  
        ordViewSource.View.Refresh();  
    }  
  
    private void DeleteOrderCommandHandler(object sender, ExecutedRoutedEventArgs e)  
    {  
        // Get the Order in the row in which the Delete button was clicked.  
        Order obj = e.Parameter as Order;  
        Delete_Order(obj);  
    }  
    ```  
  
3. 按 F5  。 您应该看到你的数据，并导航按钮应正常运行。 单击"提交"以向模型添加新客户或订单后输入的数据。  单击"取消"以退出新客户或新的订单窗体而不保存。 可以对现有客户和订单的文本框中直接进行编辑，这些更改将写入到该模型自动。  
  
## <a name="see-also"></a>请参阅  
 [适用于.NET 的 visual Studio data tools](../data-tools/visual-studio-data-tools-for-dotnet.md) [Entity Framework 文档](https://msdn.microsoft.com/data/ee712907.aspx)
