---
title: 通过 WPF 和 Entity Framework 6 的简单数据应用程序
ms.date: 08/22/2017
ms.topic: conceptual
dev_langs:
- CSharp
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: d67ca69856f48ec916f27498798cbb58efb3e5ac
ms.sourcegitcommit: 13ab9a5ab039b070b9cd9251d0b83dd216477203
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177364"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>使用 WPF 和 Entity Framework 6 创建简单的数据应用程序

本演练演示如何在 Visual Studio 中创建一个基本"forms over data"应用程序。 该应用使用 SQL Server LocalDB，Northwind 数据库、 Entity Framework 6 和 Windows Presentation Foundation。 它演示如何执行基本数据绑定的大纲-细节视图，并且也包含自定义绑定与按钮导航器**移动到下一步**，**移动上一个**，**将移到从**，**移至末尾**，**更新**并**删除**。

本文重点介绍在 Visual Studio 中，使用数据工具并不会尝试解释中任何深度的基础技术。 它假定你已基本熟悉 XAML、 实体框架和 SQL。 此示例中也并不演示模型-视图-视图模型 (MVVM) 体系结构，它是用于 WPF 应用程序的标准。 但是，可以将此代码复制到自己稍作修改的 MVVM 应用程序。

## <a name="install-and-connect-to-northwind"></a>安装并连接到 Northwind

此示例使用 SQL Server Express LocalDB 和 Northwind 示例数据库。 如果该产品的 ADO.NET 数据提供程序支持实体框架，它应同样适用于其他 SQL 数据库产品。

1. 如果您没有 SQL Server Express LocalDB，安装它从[SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)，或通过**Visual Studio 安装程序**。 在中**Visual Studio 安装程序**，可以作为的一部分安装 SQL Server Express LocalDB **.NET 桌面开发**工作负荷或作为单个组件。

2. 通过执行以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中打开**SQL Server 对象资源管理器**窗口。 (**SQL Server 对象资源管理器**的一部分安装**数据存储和处理**中的工作负荷**Visual Studio 安装程序**。)展开**SQL Server**节点。 LocalDB 实例上右键单击并选择**新查询**。

       查询编辑器窗口随即打开。

    2. 复制[Northwind Transact SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)到剪贴板。 此 T-SQL 脚本从零开始创建 Northwind 数据库，并使用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器，然后选择**Execute**按钮。

       后不久，查询完成运行并创建 Northwind 数据库。

3. [添加新连接](../data-tools/add-new-connections.md)northwind。

## <a name="configure-the-project"></a>配置项目

1. 在 Visual Studio 中，创建一个新C# **WPF 应用**项目。

2. 为 Entity Framework 6 中添加 NuGet 包。 在中**解决方案资源管理器**，选择项目节点。 在主菜单中，选择**项目** > **管理 NuGet 包**。

     ![管理 NuGet 包的菜单项](../data-tools/media/raddata_vs2015_manage_nuget_packages.png)

3. 在中**NuGet 包管理器**，单击**浏览**链接。 实体框架可能是在列表中的顶层包。 单击**安装**右窗格中，按照提示进行操作。 输出窗口会告诉您何时完成安装。

     ![实体框架 NuGet 包](../data-tools/media/raddata_vs2015_nuget_ef.png)

4. 现在可以使用 Visual Studio 来创建基于 Northwind 数据库的模型。

## <a name="create-the-model"></a>创建模型

1. 右键单击项目节点中**解决方案资源管理器**，然后选择**添加** > **新项**。 在左窗格中，在 C# 节点下，选择**数据**，然后在中间窗格中，选择**ADO.NET 实体数据模型**。

   ![实体框架模型的新项](../data-tools/media/raddata-ef-new-project-item.png)

2. 调用该模型`Northwind_model`，然后选择**确定**。 “实体数据模型”向导随即打开。 选择**EF 设计器从数据库**，然后单击**下一步**。

   ![从数据库的 EF 模型](../data-tools/media/raddata-ef-model-from-database.png)

3. 在下一个屏幕，然后单击选择 LocalDB Northwind**下一步**。

4. 在向导的下一页上，选择的表、 存储的过程和要包含在实体框架模型中其他数据库对象。 展开树视图中的 dbo 节点并选择**客户**，**订单**，并**Order Details**。 保留选中的默认值，然后单击**完成**。

    ![选择模型的数据库对象](../data-tools/media/raddata-choose-ef-objects.png)

5. 向导将生成表示实体框架模型的 C# 类。 类是普通旧的 C# 类，并且我们数据绑定到 WPF 用户界面。 *.Edmx*文件介绍了关系和其他将类与数据库中的对象相关联的元数据。 *.Tt*文件是生成的代码，运行或保存对数据库进行更改的模型的 T4 模板。 可以看到所有这些文件中的**解决方案资源管理器**Northwind_model 节点下：

      ![解决方案资源管理器 EF 模型文件](../data-tools/media/raddata-solution-explorer-ef-model-files.png)

    为设计器图面 *.edmx*文件，您可以修改一些属性和关系在模型中的。 我们不打算在本演练中使用设计器。

6. *.Tt*文件是常规用途和需要调整它们以使用 WPF 数据绑定，这要求 ObservableCollections 之一。 在中**解决方案资源管理器**，展开 Northwind_model 节点，直到找到*Northwind_model.tt*。 (请确保不在 *。Context.tt*文件，它是正下方 *.edmx*文件。)

   - 替换的两个匹配项<xref:System.Collections.ICollection>与<xref:System.Collections.ObjectModel.ObservableCollection%601>。

   - 替换为第一个匹配项<xref:System.Collections.Generic.HashSet%601>与<xref:System.Collections.ObjectModel.ObservableCollection%601>在第 51 行。 不会替代 HashSet 的第二个匹配项。

   - 替换的唯一匹配项<xref:System.Collections.Generic>（在第 431 行） 与<xref:System.Collections.ObjectModel>。

7. 按**Ctrl**+**Shift**+**B**以生成项目。 如果生成完成后，在 model 类将显示到数据源向导。

现在已准备好将挂接到此模型添加到 XAML 页，以便可以查看、 导航和修改数据。

## <a name="databind-the-model-to-the-xaml-page"></a>数据绑定到 XAML 页面模型

可以编写自己的数据绑定代码，但可让 Visual Studio 为您做容易得多。

1. 从主菜单中，选择**项目** > **添加新数据源**以打开**数据源配置向导**。 选择**对象**因为要绑定到模型类不到数据库：

     ![与对象源的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png)

2. 选择**客户**。 （订单的源会自动从生成中客户的订单导航属性。）

     ![将实体类添加为数据源](../data-tools/media/raddata-add-entity-classes-as-data-sources.png)

3. 单击 **“完成”** 。

4. 导航到*MainWindow.xaml*在代码视图中。 我们将为此示例的目的来保持 XAML 简单。 主窗口的标题更改为更具描述性和现在为 600 x 800 增加其高度和宽度。 稍后可以随时更改它。 现在将这些包含三行定义添加到主网格中，导航按钮，以多客户的详细信息，一个用于显示其订单的网格的一行：

    ```xaml
    <Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ```

5. 现在，打开*MainWindow.xaml* ，以便你正在设计器中查看它。 这将导致**数据源**窗口中显示为 Visual Studio 窗口边距中的一个选项旁边**工具箱**。 单击选项卡以打开窗口，或其他按**Shift**+**Alt**+**D**或选择**视图** > **其他 Windows** > **数据源**。 我们要在自己单独的文本的框中的客户类中显示每个属性。 首先，请单击中箭头**客户**组合框，然后选择**详细信息**。 以便在设计器知道你希望它转中间行中，然后，将节点拖到设计图面上的中间部分上。 如果您忘记放置位置，您可以以后手动在 XAML 中指定的一行。 默认情况下，控件垂直放置在网格元素中，但此时，您可以排列它们想在窗体上。 例如，可能会有用放**名称**在最前面，上面地址文本框。 这篇文章的示例应用程序对字段重新排序，并为两列中重新排列它们。

     ![为单个控件的客户数据源绑定](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png)

     在代码视图中，您现在可以看到一个新`Grid`中元素的第 1 行 （中间行） 的父网格。 网格具有的父`DataContext`属性，它引用已添加到 CollectionViewSource`Windows.Resources`元素。 提供该数据上下文，当第一个文本框中将绑定到**地址**，该名称映射到`Address`属性在当前`Customer`CollectionViewSource 中的对象。

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. 客户在窗口的上半部分中可见时，想要查看其底部中的订单半双工。 在单个网格视图控件中显示的订单。 按预期方式工作的大纲-细节数据绑定，务必绑定到客户类，不到单独的订单节点中的 Orders 属性。 将客户类的 Orders 属性拖动到窗体的下半部分，以便在设计器将其放入第 2 行：

     ![为网格拖动订单类](../data-tools/media/raddata-drag-orders-classes-as-grid.png)

7. Visual Studio 已生成连接到模型中的事件的 UI 控件的所有绑定代码。 您需要执行的操作，请参阅一些数据，只需编写一些代码来填充模型。 首先，导航到*MainWindow.xaml.cs*并将数据成员添加到 MainWindow 类中的数据上下文。 已为你生成，此对象的作用类似于跟踪的更改，并在模型中的事件的控件的内容。 此外将添加构造函数初始化逻辑。 类的顶部应如下所示：

     [!code-csharp[MainWindow#1](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#1)]

     添加`using`指令 System.Data.Entity 将 Load 扩展方法引入作用域：

     ```csharp
     using System.Data.Entity;
     ```

     现在，向下滚动并找到`Window_Loaded`事件处理程序。 请注意，Visual Studio 添加了 CollectionViewSource 对象。 这表示当您在创建模型时所选择的 NorthwindEntities 对象。 让我们将代码添加到`Window_Loaded`，以便整个方法现在如下所示：

     [!code-csharp[Window_Loaded#2](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#2)]

8. 按 F5 。 你应该看到已检索到 CollectionViewSource 的第一个客户的详细信息。 您还应该看到他们在数据网格中的订单。 格式设置不是太好了，因此让我们来修复的。 此外可以创建一种方法，以查看其他记录并执行基本的 CRUD 操作。

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>调整页面设计并添加新客户和订单的网格

Visual Studio 生成的默认排列方式是不适合您的应用程序，因此你将在 XAML 中手动进行一些更改。 您还需要一些"forms"（这是实际网格），使用户能够添加新客户或订单。 为了能够添加新客户和订单，需要一组单独的不是数据绑定到的文本框`CollectionViewSource`。 将控制哪些用户会看到在任何给定时间通过将 Visible 属性设置的处理程序方法中的网格。 最后，将删除按钮添加到订单网格以使用户能够删除各个订单中每个行。

首先，将添加到这些样式`Windows.Resources`中的元素*MainWindow.xaml*:

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
<Grid>
     <Grid.RowDefinitions>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="*"/>
     </Grid.RowDefinitions>
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
         <TextBox x:Name="customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
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
         <TextBox x:Name="add_customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true }"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
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
                         <Button Content="Delete" Command="{StaticResource DeleteOrderCommand}" CommandParameter="{Binding}"/>
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

在 Windows 窗体应用程序中的数据库中的行中导航并执行基本的 CRUD 操作获取具有按钮的 BindingNavigator 对象。 WPF 不提供 BindingNavigator，但它很容易地创建一个。 使用按钮内的水平的 StackPanel，执行该操作并将这些按钮与绑定到方法后面的代码中的命令相关联。

有个 4 命令逻辑部分：（1） 命令、 （2） 绑定、 （3) 按钮和隐藏代码中 （4） 的命令处理程序。

### <a name="add-commands-bindings-and-buttons-in-xaml"></a>在 XAML 中添加命令、 绑定和按钮

1. 首先，添加中的命令*MainWindow.xaml*文件内`Windows.Resources`元素：

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

2. CommandBinding 映射`RoutedUICommand`背后的代码中的方法的事件。 添加以下`CommandBindings`元素后的`Windows.Resources`结束标记：

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

3. 现在，添加`StackPanel`与导航窗格中，添加、 删除和更新按钮。 首先，将添加到此样式`Windows.Resources`:

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     其次，将此代码粘贴到紧`RowDefinitions`外部`Grid`元素中，XAML 页面的顶部附近：

    ```xaml
    <StackPanel Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">
        <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnPrev" Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnNext" Content="►" Command="{StaticResource NextCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnLast" Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>
        <Button Name="btnAdd" Content="New Customer" Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>
        <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="Cancel" Name="btnCancel" Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
    </StackPanel>
    ```

### <a name="add-command-handlers-to-the-mainwindow-class"></a>向 MainWindow 类中添加命令处理程序

代码隐藏很小的添加和删除方法除外。 通过 CollectionViewSource 视图属性上调用方法来执行导航。 `DeleteOrderCommandHandler`演示如何在订单执行级联删除。 我们必须先删除与之关联 Order_Details。 `UpdateCommandHandler`将新客户或订单添加到集合，否则只需与用户在文本框中所做的更改更新现有客户或订单。

向 MainWindow 类中添加这些处理程序方法*MainWindow.xaml.cs*。 如果你 CollectionViewSource 为 Customers 表具有不同的名称，然后您需要调整中的每个这些方法的名称：

[!code-csharp[CommandHandlers#3](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#3)]

## <a name="run-the-application"></a>运行此应用程序

若要启用调试，请按 F5。 你应看到客户和订单数据在网格中，填充和导航按钮应正常运行。 单击**提交**向模型添加新客户或订单后输入的数据。 单击**取消**后退新客户或新的订单窗体而不保存数据。 可以对现有客户和订单的文本框中直接进行编辑，这些更改将自动写入模型。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [实体框架文档](/ef/)