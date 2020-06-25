---
title: 带有 WPF 和实体框架6的简单数据应用程序
ms.date: 08/22/2017
ms.topic: conceptual
dev_langs:
- CSharp
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4aa978098c459d9e55ef0dc1423080357e067a5b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282756"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>使用 WPF 和 Entity Framework 6 创建简单的数据应用程序

本演练演示如何在 Visual Studio 中创建基本的 "窗体 over 数据" 应用程序。 应用使用 SQL Server LocalDB、Northwind 数据库、实体框架6（非 Entity Framework Core）和 .NET Framework 的 Windows Presentation Foundation （而非 .NET Core）。 它演示了如何使用大纲-详细信息视图进行基本数据绑定，还提供了一个自定义绑定导航器，其中包含用于**移动**的按钮、"**上**移"、"移**至开头**"、"**结束**"、"**更新**" 和 "**删除**"。

本文重点介绍如何在 Visual Studio 中使用数据工具，并且不会尝试深入了解底层技术。 假设您基本熟悉 XAML、实体框架和 SQL。 此示例还不演示模型-视图-ViewModel （MVVM）体系结构，这是 WPF 应用程序的标准。 不过，你可以将此代码复制到你自己的 MVVM 应用程序中，只需修改少量内容。

## <a name="install-and-connect-to-northwind"></a>安装并连接到 Northwind

此示例使用 SQL Server Express LocalDB 和 Northwind 示例数据库。 如果该产品的 ADO.NET 数据提供程序支持实体框架，则它也适用于其他 SQL 数据库产品。

1. 如果没有 SQL Server Express 的 LocalDB，请从[SQL Server Express 下载 "页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过**Visual Studio 安装程序**安装它。 在 Visual Studio 安装程序中，可将 SQL Server Express LocalDB 作为 .NET 桌面开发工作负载的一部分安装，也可作为单独组件安装********。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 " **SQL Server 对象资源管理器**" 窗口。 （**SQL Server 对象资源管理器**作为**Visual Studio 安装程序**中的**数据存储和处理**工作负荷的一部分安装。）展开 " **SQL Server** " 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    2. 将[Northwind transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-sql 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    3. 将 T-sql 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询将完成运行，并创建 Northwind 数据库。

3. 为 Northwind[添加新连接](../data-tools/add-new-connections.md)。

## <a name="configure-the-project"></a>配置项目

1. 在 Visual Studio 中，创建一个新的 c # **WPF 应用程序**项目。

2. 为实体框架6添加 NuGet 包。 在**解决方案资源管理器**中，选择 "项目" 节点。 在主菜单中，选择 "**项目**" "  >  **管理 NuGet 包**"。

     !["管理 NuGet 包" 菜单项](../data-tools/media/raddata_vs2015_manage_nuget_packages.png)

3. 在**NuGet 包管理器**中，单击 "**浏览**" 链接。 实体框架可能是列表中的顶层包。 单击右窗格中的 "**安装**"，并按照提示进行操作。 "输出" 窗口将显示安装完成的时间。

     ![实体框架 NuGet 包](../data-tools/media/raddata_vs2015_nuget_ef.png)

4. 现在，可以使用 Visual Studio 创建基于 Northwind 数据库的模型。

## <a name="create-the-model"></a>创建模型

1. 右键单击 "**解决方案资源管理器**中的项目节点，然后选择"**添加**  >  **新项**"。 在左窗格中的 "c #" 节点下，选择 "**数据**"，然后在中间窗格中选择 " **ADO.NET 实体数据模型**"。

   ![实体框架为新项建模](../data-tools/media/raddata-ef-new-project-item.png)

2. 调用模型 `Northwind_model` ，然后选择 **"确定"**。 **实体数据模型向导**将打开。 **从数据库中选择 EF 设计器**，然后单击 "**下一步**"。

   ![数据库中的 EF 模型](../data-tools/media/raddata-ef-model-from-database.png)

3. 在下一个屏幕中，输入或选择 LocalDB Northwind 连接（例如，（LocalDB） \MSSQLLocalDB），指定 Northwind 数据库，然后单击 "**下一步**"。

4. 在向导的下一页上，选择要包含在实体框架模型中的表、存储过程和其他数据库对象。 展开树视图中的 "dbo" 节点，然后选择 "**客户**"、"**订单**" 和 "**订单详细信息**"。 保留默认选中状态，并单击 "**完成**"。

    ![为模型选择数据库对象](../data-tools/media/raddata-choose-ef-objects.png)

5. 向导将生成表示实体框架模型的 c # 类。 类是普通的旧 c # 类，并且是我们在 WPF 用户界面中进行 databind 的。 *.Edmx*文件描述了关联类与数据库中的对象的其他元数据。 *Tt*文件是 T4 模板，用于生成对模型进行操作并将更改保存到数据库的代码。 可以在 "Northwind_model" 节点下**解决方案资源管理器**查看所有这些文件：

      ![解决方案资源管理器 EF 模型文件](../data-tools/media/raddata-solution-explorer-ef-model-files.png)

    *.Edmx*文件的设计器图面使你可以修改模型中的某些属性和关系。 在本演练中，我们不打算使用设计器。

6. *Tt*文件是常规用途，你需要调整其中一个文件以使用 WPF 数据绑定，这需要 ObservableCollections。 在**解决方案资源管理器**中，展开 "Northwind_model" 节点，直到找到 " *Northwind_model"。* （确保你不在中 *。Context.tt*文件，它位于 *.edmx*文件的正下方。）

   - 将的两个匹配项替换 <xref:System.Collections.ICollection> 为 <xref:System.Collections.ObjectModel.ObservableCollection%601> 。

   - 将的第一个匹配项替换 <xref:System.Collections.Generic.HashSet%601> 为第 <xref:System.Collections.ObjectModel.ObservableCollection%601> 51 行。 请勿替换第二次出现的 HashSet。

   - 将唯一匹配项 <xref:System.Collections.Generic> （约431行）替换为 <xref:System.Collections.ObjectModel> 。

7. 按**Ctrl** + **Shift** + **B**生成项目。 当生成完成时，这些模型类对于 "数据源向导" 可见。

现在您已准备好将此模型挂接到 XAML 页，以便您可以查看、导航和修改数据。

## <a name="databind-the-model-to-the-xaml-page"></a>将模型 Databind 到 XAML 页

可以编写自己的数据绑定代码，但使 Visual Studio 可以更轻松地为你执行此操作。

1. 从主菜单中，选择 "**项目**  >  " "**添加新数据源**" 以打开 "**数据源配置向导**"。 选择 "**对象**"，因为您要绑定到模型类，而不是绑定到数据库：

     ![具有对象源的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png)

2. 展开项目的节点，然后选择 "**客户**"。 （订单的源自动从 Customer 的 Orders 导航属性生成。）

     ![添加实体类作为数据源](../data-tools/media/raddata-add-entity-classes-as-data-sources.png)

3. 单击“完成”。

4. 在代码视图中导航到*mainwindow.xaml* 。 出于本示例的目的，我们将保持 XAML 简单。 将 Mainwindow.xaml 的标题更改为更具描述性的名称，并将其高度和宽度增加为 600 x 800。 以后随时可以更改它。 现在，将这三个行定义添加到主网格，一行用于导航按钮，一个用于客户的详细信息，一个用于显示其订单的网格：

    ```xaml
        <Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ```

5. 现在打开*mainwindow.xaml* ，以便在设计器中查看它。 这会导致 "**数据源**" 窗口在 "**工具箱**" 旁边的 Visual Studio 窗口边距中显示为一个选项。 单击该选项卡以打开窗口，或者按**Shift** + **Alt** + **D**或选择 "**查看**  >  **其他 Windows**  >  **数据源**"。 我们会将 Customers 类中的每个属性都显示在单独的文本框中。 首先，单击 "**客户**" 组合框中的箭头，然后选择 "**详细信息**"。 然后，将节点拖动到设计图面的中间部分，以便设计器知道您希望它进入中间行。 如果丢失，则可以在 XAML 中以后手动指定该行。 默认情况下，控件在网格元素中垂直放置，但此时，您可以在窗体上对其进行排列。 例如，将 "**名称**" 文本框放在地址上方时，可能有意义。 本文的示例应用程序将对字段重新排序，并将其重新排列为两列。

     ![客户数据源绑定到各个控件](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png)

     在代码视图中，现在可以 `Grid` 在父网格的第1行（中间行）中看到一个新元素。 父网格具有一个 `DataContext` 属性，该属性引用已添加到元素中的 CollectionViewSource `Windows.Resources` 。 假设该数据上下文在第一个文本框绑定到**Address**时，该名称将映射到 `Address` CollectionViewSource 中当前对象的属性 `Customer` 。

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. 当客户在窗口的上半部分可见时，您希望在下半部分查看其订单。 在单个网格视图控件中显示订单。 若要使主/从数据绑定按预期工作，请务必绑定到 Customers 类中的 Orders 属性，而不是绑定到单独的 "订单" 节点。 将 Customers 类的 Orders 属性拖到窗体的下半部分，以便设计器将其放在第2行：

     ![将 Orders 类作为网格拖动](../data-tools/media/raddata-drag-orders-classes-as-grid.png)

7. Visual Studio 生成了将 UI 控件连接到模型中的事件的所有绑定代码。 若要查看某些数据，你只需编写一些代码来填充模型。 首先，导航到*MainWindow.xaml.cs* ，并将数据成员添加到数据上下文的 mainwindow.xaml 类。 已为您生成的此对象的行为类似于跟踪模型中的更改和事件的控件。 你还将为客户和订单添加 CollectionViewSource 数据成员和关联的构造函数初始化逻辑。 类的顶部应如下所示：

     [!code-csharp[MainWindow#1](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#1)]

     为 system.string 添加 `using` 指令以将负载扩展方法添加到作用域中：

     ```csharp
     using System.Data.Entity;
     ```

     现在，向下滚动并找到 `Window_Loaded` 事件处理程序。 请注意，Visual Studio 已添加 CollectionViewSource 对象。 这表示创建模型时选择的 NorthwindEntities 对象。 您已经添加了该程序，因此您不需要这样做。 让我们替换中的代码， `Window_Loaded` 使方法现在如下所示：

     [!code-csharp[Window_Loaded#2](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#2)]

8. 按 **F5**。 应会看到检索到 CollectionViewSource 中的第一个客户的详细信息。 还应在数据网格中看到它们的顺序。 格式设置不是很好，因此让我们来解决这个问题。 您还可以创建一种方法来查看其他记录并执行基本的 CRUD 操作。

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>调整页面设计并为新客户和订单添加网格

Visual Studio 生成的默认布局并非适用于你的应用程序，因此我们将在此处提供最终 XAML 以复制到你的代码中。 还需要某些 "窗体" （实际上是网格），以使用户能够添加新客户或订单。 为了能够添加新的客户和订单，您需要一组不是数据绑定到的单独的文本框 `CollectionViewSource` 。 通过在处理程序方法中设置 Visible 属性，可以控制用户在任意给定时间看到的网格。 最后，将 "删除" 按钮添加到 "订单" 网格中的每一行，以使用户能够删除单个订单。

首先，将这些样式添加到 `Windows.Resources` *mainwindow.xaml*中的元素：

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

接下来，将整个外部网格替换为以下标记：

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

## <a name="add-buttons-to-navigate-add-update-and-delete"></a>添加用于导航、添加、更新和删除的按钮

在 Windows 窗体应用程序中，您将获得一个 BindingNavigator 对象，其中包含用于在数据库中的行间导航并执行基本 CRUD 操作的按钮。 WPF 并不提供 BindingNavigator，但可以很容易创建一个。 使用水平 System.windows.controls.stackpanel> 中的按钮执行该操作，并将这些按钮与代码隐藏中的方法绑定的命令相关联。

命令逻辑有四个部分：（1）个命令，（2）个绑定，（3）个按钮，以及（4）代码隐藏中的命令处理程序。

### <a name="add-commands-bindings-and-buttons-in-xaml"></a>在 XAML 中添加命令、绑定和按钮

1. 首先，将*mainwindow.xaml*文件中的命令添加到 `Windows.Resources` 元素中：

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

2. System.windows.input.commandbinding> 将事件映射 `RoutedUICommand` 到代码隐藏中的方法。 将此 `CommandBindings` 元素添加到 `Windows.Resources` 结束标记后：

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

3. 现在，请将添加到 " `StackPanel` 导航"、"添加"、"删除" 和 "更新" 按钮。 首先，将以下样式添加到 `Windows.Resources` ：

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     然后，将此代码粘贴到紧邻 `RowDefinitions` `Grid` XAML 页顶部的外部元素之后：

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

### <a name="add-command-handlers-to-the-mainwindow-class"></a>向 Mainwindow.xaml 类添加命令处理程序

除 add 和 delete 方法外，代码隐藏是最少的。 通过对 CollectionViewSource 的 View 属性调用方法来执行导航。 `DeleteOrderCommandHandler`演示如何对订单执行级联删除。 我们必须先删除与之关联的 Order_Details。 向 `UpdateCommandHandler` 集合中添加新的客户或订单，或者只是使用用户在文本框中做出的更改来更新现有客户或订单。

将这些处理程序方法添加到*MainWindow.xaml.cs*中的 mainwindow.xaml 类。 如果 "客户" 表的 CollectionViewSource 具有不同的名称，则需要调整其中每个方法中的名称：

[!code-csharp[CommandHandlers#3](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#3)]

## <a name="run-the-application"></a>运行应用程序

若要启用调试，请按 F5****。 应会看到 "客户" 和 "订单" 数据已填充到网格中，导航按钮应按预期方式工作。 在输入数据后，单击 "**提交**" 将新客户或订单添加到模型。 单击 "**取消**" 以从新客户或新订单窗体中返回，而不保存数据。 您可以直接在文本框中编辑现有客户和订单，这些更改会自动写入到模型中。

## <a name="see-also"></a>另请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [实体框架文档](/ef/)
