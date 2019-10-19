---
title: 将 WPF 控件绑定到数据集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 177420b9-568b-4dad-9d16-1b0e98a24d71
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 70dfaa5671f589c02560a554a6d50611c5364c82
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651188"
---
# <a name="bind-wpf-controls-to-a-dataset"></a>将 WPF 控件绑定到数据集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，你将创建一个包含数据绑定控件的 WPF 应用程序。 这些控件将绑定到在数据集中封装的产品记录。 你还将添加用于浏览产品和保存对产品记录所做的更改的按钮。

 本演练阐释了以下任务：

- 创建一个 WPF 应用程序和一个利用 AdventureWorksLT 示例数据库中的数据生成的数据集。

- 通过将数据表从“数据源”窗口拖到 WPF 设计器的窗口中，创建一组数据绑定控件。

- 创建用于向前/向后导航产品记录的按钮。

- 创建一个用于将用户对产品记录所做的更改保存到数据表和基础数据源的按钮。

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Prerequisites
 你需要以下组件来完成本演练：

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]

- 对附加了 AdventureWorksLT 示例数据库的 SQL Server 或 SQL Server Express 的正在运行的实例的访问权限。 可以从[CodePlex](http://go.microsoft.com/fwlink/?linkid=87843)网站下载 AdventureWorksLT 数据库。

  事先了解以下概念也很有用，但对于完成本演练并不是必需的：

- 数据集和 TableAdapter。 有关详细信息，请参阅[Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。

- 使用 WPF 设计器。 有关详细信息，请参阅[WPF 和 Silverlight 设计器概述](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)。

- WPF 数据绑定。 有关详细信息，请参阅 [数据绑定概述](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)。

## <a name="create-the-project"></a>创建项目
 创建一个新的 WPF 项目。 该项目将显示产品记录。

#### <a name="to-create-the-project"></a>要创建项目

1. 启动 Visual Studio。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

3. 展开“Visual Basic”或“Visual C#”，然后选择“Windows”。

4. 选择“WPF 应用程序”项目模板。

5. 在 "**名称**" 框中，键入 `AdventureWorksProductsEditor` 然后单击 **"确定"** 。

     Visual Studio 将创建 `AdventureWorksProductsEditor` 项目。

## <a name="create-a-dataset-for-the-application"></a>为应用程序创建数据集
 必须先为应用程序定义数据模型并将此模型添加到“数据源”窗口中，然后才能创建数据绑定控件。 在本演练中，你将创建要用作数据模型的数据集。

#### <a name="to-create-a-dataset"></a>创建数据集

1. 在 **“数据”** 菜单上，单击 **“显示数据源”** 。

     “数据源”窗口随即打开。

2. 在 **“数据源”** 窗口中，单击 **“添加新数据源”** 。

     “数据源配置”向导随即打开。

3. 在“选择数据源类型”页上，选择“数据库”，然后单击“下一步”。

4. 在“选择数据库模型”页上，选择“数据集”，然后单击“下一步”。

5. 在“选择你的数据连接”页面上，选择以下选项之一：

    - 如果下拉列表中包含到 AdventureWorksLT 示例数据库的数据连接，请选择该连接，然后单击“下一步”。

    - 单击“新建连接”，然后创建到 AdventureWorksLT 数据库的连接。

6. 在“将连接字符串保存到应用程序配置文件中”页面上，选中“是，将连接另存为”复选框，然后单击“下一步”。

7. 在“选择数据库对象”页面上，展开“表”，然后选择“Product (SalesLT)”表。

8. 单击 **“完成”** 。

     Visual Studio 会向项目中添加一个新的 Adventureworksltdataset.xsd 文件，并将相应的**adventureworksltdataset.xsd**项添加到 "**数据源**" 窗口。 AdventureWorksLTDataSet.xsd 文件定义了一个名为 `AdventureWorksLTDataSet` 的类型化数据集和一个名为 `ProductTableAdapter` 的 TableAdapter。 在本演练后面的部分中，你将使用 `ProductTableAdapter` 向数据集填充数据，并将更改保存回数据库中。

9. 生成项目。

## <a name="edit-the-default-fill-method-of-the-tableadapter"></a>编辑 TableAdapter 的默认填充方法
 若要向数据集填充数据，请使用 `Fill` 的 `ProductTableAdapter` 方法。 默认情况下，`Fill` 方法将向 `ProductDataTable` 中的 `AdventureWorksLTDataSet` 填充 Product 表包含的所有数据行。 你可以修改此方法以仅返回行的子集。 对于本演练而言，将修改 `Fill` 方法以仅返回具有照片的产品行。

#### <a name="to-load-product-rows-that-have-photos"></a>加载具有照片的产品行

1. 在**解决方案资源管理器**中，双击 adventureworksltdataset.xsd 文件。

     这将打开数据集设计器。

2. 在设计器中，右键单击 "**填充"、""，** 然后选择 "**配置**"。

     “TableAdapter 配置”向导随即打开。

3. 在“输入 SQL 语句”页面上，在文本框中的 `SELECT` 语句后添加以下 WHERE 子句。

    ```
    WHERE ThumbnailPhotoFileName <> 'no_image_available_small.gif'
    ```

4. 单击 **“完成”** 。

## <a name="define-the-user-interface"></a>定义用户界面
 通过在 WPF 设计器中修改 XAML，将多个按钮添加到该窗口中。 在本演练后面的部分中，你将添加可让用户通过使用这些按钮来滚动和保存对产品记录所做的更改的代码。

#### <a name="to-define-the-user-interface-of-the-window"></a>定义窗口的用户界面

1. 在**解决方案资源管理器**中，双击 "mainwindow.xaml"。

     将在 WPF 设计器中打开相应的窗口。

2. 在设计器的 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 视图中，在 `<Grid>` 标记之间添加以下代码：

    ```
    <Grid.RowDefinitions>
        <RowDefinition Height="75" />
        <RowDefinition Height="625" />
    </Grid.RowDefinitions>
    <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75"><</Button>
    <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">></Button>
    <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>
    ```

3. 生成项目。

## <a name="createdata-bound-controls"></a>Createdata 绑定控件
 通过将 `Product` 表从 "**数据源**" 窗口拖到 WPF 设计器，创建显示客户记录的控件。

#### <a name="to-create-data-bound-controls"></a>创建数据绑定控件

1. 在“数据源”窗口中，单击“Product”节点的下拉菜单，然后选择“详细信息”。

2. 展开“Product”节点。

3. 在本示例中，某些字段不会显示，因此只需单击下列节点旁边的下拉菜单，然后选择“无”：

    - ProductCategoryID

    - ProductModelID

    - ThumbnailPhotoFileName

    - rowguid

    - ModifiedDate

4. 单击“ThumbNailPhoto”节点旁边的下拉菜单，然后选择“图像”。

    > [!NOTE]
    > 默认情况下，已将“数据源”窗口中表示图片的项的默认控件设置为“无”。 这是因为，图片是作为字节数组存储在数据库中的，并且从简单的字节数组到大型应用程序的可执行文件都可以包含在字节数组中。

5. 从“数据源”窗口，将“Product”节点拖到包含按钮的行下方的网格行。

     Visual Studio 生成 XAML，它定义了一组绑定到“Products”表中的数据的控件。 它还会生成用于加载数据的代码。 有关生成的 XAML 和代码的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

6. 在设计器中，单击“Product ID”标签旁边的文本框。

7. 在“属性”窗口，选中“IsReadOnly”属性旁边的复选框。

## <a name="navigating-product-records"></a>导航产品记录
 添加可让用户通过“\<”和“>”按钮来浏览产品记录的代码。

#### <a name="to-enable-users-to-navigate-product-records"></a>使用户能够导航产品记录

1. 在设计器中，双击窗口窗面上的“<”按钮。

     Visual Studio 打开代码隐藏文件，并为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件创建新的 `backButton_Click` 事件处理程序。

2. 修改 `Window_Loaded` 事件处理程序，使 `ProductViewSource`、`AdventureWorksLTDataSet` 和 `AdventureWorksLTDataSetProductTableAdapter` 位于该方法的外部，并使它们在整个窗体中可访问。 仅将这些项声明为全局窗体，并将它们分配到 `Window_Loaded` 事件处理程序中，如下所示：

     [!code-csharp[Data_WPFDATASET#1](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#1)]
     [!code-vb[Data_WPFDATASET#1](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#1)]

3. 将以下代码添加到 `backButton_Click` 事件处理程序中：

     [!code-csharp[Data_WPFDATASET#2](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#2)]
     [!code-vb[Data_WPFDATASET#2](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#2)]

4. 返回到设计器，然后双击“>”按钮。

5. 将以下代码添加到 `nextButton_Click` 事件处理程序中：

     [!code-csharp[Data_WPFDATASET#3](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#3)]
     [!code-vb[Data_WPFDATASET#3](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#3)]

## <a name="savechanges-to-product-records"></a>与产品记录的 Savechanges
 添加代码，该代码可让用户通过使用“保存更改”按钮来保存对产品记录所做的更改。

#### <a name="to-add-the-ability-to-save-changes-to-product-records"></a>添加保存对产品记录所做更改的功能

1. 在设计器中，双击“保存更改”按钮。

     Visual Studio 打开代码隐藏文件，并为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件创建新的 `saveButton_Click` 事件处理程序。

2. 将以下代码添加到 `saveButton_Click` 事件处理程序中：

     [!code-csharp[Data_WPFDATASET#4](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#4)]
     [!code-vb[Data_WPFDATASET#4](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#4)]

    > [!NOTE]
    > 此示例使用 `Save` 的 `TableAdapter` 方法来保存更改。 这对于本演练很合适，因为本演练中只会更改一个数据表。 如果你需要保存对多个数据表所做的更改，则还可以使用 Visual Studio 利用你的数据集生成的 `UpdateAll` 的 `TableAdapterManager` 方法。 有关详细信息，请参阅[TableAdapterManager 概述](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)。

## <a name="test-the-application"></a>测试应用程序
 生成并运行应用程序。 验证你是否可以查看和更新产品记录。

#### <a name="to-test-the-application"></a>测试应用程序

1. 按 F5。

     这将生成并运行应用程序。 验证以下内容：

    - 文本框显示具有图片的第一条产品记录的数据。 此产品的产品 ID 为 713，名称为“Long-Sleeve Logo Jersey, S”。

    - 可以单击“>”或“<”按钮来导航其他产品记录。

2. 在某一产品记录中，更改“大小”值，然后依次“保存更改”。

3. 关闭该应用程序，然后在 Visual Studio 中按 F5 重启该应用程序。

4. 导航到已更改的产品记录，然后验证是否已保存更改。

5. 关闭该应用程序。

## <a name="next-steps"></a>后续步骤
 完成本演练后，你可以执行以下相关任务：

- 了解如何使用 Visual Studio 中的“数据源”窗口将 WPF 控件绑定到其他类型的数据源上。 有关详细信息，请参阅[将 WPF 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)。

- 了解如何使用 Visual Studio 中的“数据源”窗口在 WPF 控件中显示相关数据（即父-子关系中的数据）。 有关详细信息，请参阅[演练：在 WPF 应用程序中显示相关数据](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)。

## <a name="see-also"></a>请参阅
 在 visual studio 中[将 wpf 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)在 visual studio 中[将 wpf 控件绑定到 visual](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md) studio 数据[集中的工具](../data-tools/dataset-tools-in-visual-studio.md) [Wpf 和 Silverlight 设计器概述](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)[数据绑定概述](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)
