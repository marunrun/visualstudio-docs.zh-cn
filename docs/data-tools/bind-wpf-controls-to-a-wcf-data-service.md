---
title: 将 WPF 控件绑定到 WCF 数据服务
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 8823537c-82f0-41f7-bf30-705f0e5e59fd
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 7371e08925ad9227cf15a93a339e6e0ed36d11db
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282847"
---
# <a name="bind-wpf-controls-to-a-wcf-data-service"></a>将 WPF 控件绑定到 WCF 数据服务

在本演练中，你将创建一个包含数据绑定控件的 WPF 应用程序。 这些控件将绑定到 WCF 数据服务中封装的客户记录。 你还将添加客户可用于查看和更新记录的按钮。

本演练阐释了以下任务：

- 创建一个利用 AdventureWorksLT 示例数据库中的数据生成的实体数据模型。

- 创建一个将实体数据模型中的数据公开给 WPF 应用程序的 WCF 数据服务。

- 通过将项从“数据源”窗口拖到 WPF 设计器来创建一组数据绑定控件****。

- 创建用于向前/向后导航客户记录的按钮。

- 创建一个按钮，用于将对控件中的数据所做的更改保存到 WCF 数据服务和基础数据源。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- Visual Studio

- 对附加了 AdventureWorksLT 示例数据库的 SQL Server 或 SQL Server Express 的正在运行的实例的访问权限。 可以从[CodePlex 网站](https://archive.codeplex.com/?p=SqlServerSamples)下载 AdventureWorksLT 数据库。

事先了解以下概念也很有用，但对于完成本演练并不是必需的：

- [WCF 数据服务](/dotnet/framework/data/wcf/wcf-data-services-overview)。

- [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 中的数据模型。

- 实体数据模型和 ADO.NET 实体框架。 有关详细信息，请参阅[实体框架概述](/dotnet/framework/data/adonet/ef/overview)。

- WPF 数据绑定。 有关详细信息，请参阅[数据绑定概述](/dotnet/desktop-wpf/data/data-binding-overview)。

## <a name="create-the-service-project"></a>创建服务项目

1. 通过创建 c # 或 Visual Basic **ASP.NET Web 应用程序**项目开始本演练。 将项目命名为**AdventureWorksService**。

2. 在“解决方案资源管理器”中，右键单击“Default.aspx”，然后选择“删除”************。 本演练不需要此文件。

## <a name="create-an-entity-data-model-for-the-service"></a>为服务创建实体数据模型

若要使用 WCF 数据服务向应用程序公开数据，您必须为该服务定义一个数据模型。 WCF 数据服务支持两种类型的数据模型：实体数据模型和使用实现接口的公共语言运行时（CLR）对象定义的自定义数据模型 <xref:System.Linq.IQueryable%601> 。 在本演练中，你将为该数据模型创建一个实体数据模型。

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在“已安装的模板”列表中，单击“数据”，然后选择“ADO.NET 实体数据模型”项目项********。

3. 将名称更改为 `AdventureWorksModel.edmx` ，然后单击 "**添加**"。

     “实体数据模型”向导随即打开****。

4. 在“选择模型内容”页面上，单击“从数据库生成”，然后单击“下一步”************。

5. 在“选择你的数据连接”页面上，选择以下选项之一****：

    - 如果下拉列表中包含到 AdventureWorksLT 示例数据库的数据连接，请选择该连接。

    - 单击“新建连接”，然后创建到 AdventureWorksLT 数据库的连接****。

6. 在“选择数据连接”页面上，确保选中了“将 App.Config 中的实体连接设置另存为”选项，然后单击“下一步”************。

7. 在“选择数据库对象”页面上，展开“表”，然后选择“SalesOrderHeader”表************。

8. 单击“完成”。

## <a name="create-the-service"></a>创建服务

创建一个 WCF 数据服务，用于向 WPF 应用程序公开实体数据模型中的数据：

1. 在“项目”**** 菜单上，选择“添加新项”****。

2. 在“已安装的模板”列表中，单击“Web”，然后选择“WCF Data Service”项目项************。

3. 在 "**名称**" 框中键入 `AdventureWorksService.svc` ，然后单击 "**添加**"。

     Visual Studio 将添加 `AdventureWorksService.svc` 到项目。

## <a name="configure-the-service"></a>配置服务

必须配置该服务，才能操作所创建的实体数据模型：

1. 在 `AdventureWorks.svc` 代码文件中，将**AdventureWorksService**类声明替换为以下代码。

     [!code-csharp[Data_WPFWCF#1](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_1.cs)]
     [!code-vb[Data_WPFWCF#1](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_1.vb)]

     此代码将更新**AdventureWorksService**类，以便它派生自在 <xref:System.Data.Services.DataService%601> `AdventureWorksLTEntities` 实体数据模型中的对象上下文类上运行的。 此代码还将更新 `InitializeService` 方法，以使服务的客户端具有对 `SalesOrderHeader` 实体的完全读/写访问权限。

2. 生成项目，并确认生成过程中未发生错误。

## <a name="create-the-wpf-client-application"></a>创建 WPF 客户端应用程序

若要显示 WCF 数据服务中的数据，请使用基于该服务的数据源创建一个新的 WPF 应用程序。 在本演练后面的部分中，你将向该应用程序中添加数据绑定控件。

1. 在“解决方案资源管理器”中，右键单击解决方案节点、单击“添加”，然后选择“新建项目”************。

2. 在“新建项目”对话框中，展开“Visual C#”或“Visual Basic”，然后选择“Windows”****************。

3. 选择“WPF 应用程序”项目模板****。

4. 在“名称”框中，键入 `AdventureWorksSalesEditor`，然后单击“确定”。********

   Visual Studio 会将 `AdventureWorksSalesEditor` 项目添加到解决方案中。

5. 在 **“数据”** 菜单上，单击 **“显示数据源”**。

   “数据源”窗口随即打开****。

6. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

   "**数据源配置**向导" 将打开。

7. 在该向导的“选择数据源类型”页面上，选择“服务”，然后单击“下一步”************。

8. 在 **“添加服务引用”** 对话框中，单击 **“发现”**。

   Visual Studio 会在当前解决方案中搜索可用服务，并将添加 `AdventureWorksService.svc` 到 "**服务**" 框中的可用服务列表。

9. 在“命名空间”框中，键入“AdventureWorksService”********。

10. 在“服务”框中，单击“AdventureWorksService.svc”，然后单击“确定”************。

    Visual Studio 下载该服务信息，然后返回到“数据源配置”向导****。

11. 在“添加服务引用”页面上，单击“完成”********。

    Visual Studio 会将表示该服务返回的数据的节点添加到“数据源”窗口中****。

## <a name="define-the-user-interface"></a>定义用户界面

通过在 WPF 设计器中修改 XAML，将多个按钮添加到该窗口中。 在本演练后面的部分中，你将添加可让用户通过使用这些按钮来查看和更新销售记录的代码。

1. 在**解决方案资源管理器**中，双击 " **mainwindow.xaml**"。

   将在 WPF 设计器中打开相应的窗口。

2. 在设计器的 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 视图中，在 `<Grid>` 标记之间添加以下代码：

   ```xaml
   <Grid.RowDefinitions>
       <RowDefinition Height="75" />
       <RowDefinition Height="525" />
   </Grid.RowDefinitions>
   <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75"><</Button>
   <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">></Button>
   <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>
   ```

3. 生成项目。

## <a name="create-the-data-bound-controls"></a>创建数据绑定控件

通过 `SalesOrderHeaders` 将节点从 "**数据源**" 窗口拖到设计器来创建显示客户记录的控件。

1. 在“数据源”窗口中，单击“SalesOrderHeaders”节点的下拉菜单，然后选择“详细信息”************。

2. 展开“SalesOrderHeaders”节点****。

3. 在本示例中，某些字段不会显示，因此只需单击下列节点旁边的下拉菜单，然后选择“无”****：

    - **CreditCardApprovalCode**

    - **ModifiedDate**

    - **OnlineOrderFlag**

    - **RevisionNumber**

    - **rowguid**

    此操作将阻止 Visual Studio 在下一步中为这些节点创建数据绑定控件。 对于本演练，假设最终用户不需要查看此数据。

4. 从“数据源”窗口中，将“SalesOrderHeaders”节点拖到包含按钮的行的下方的网格行********。

     Visual Studio 将生成 XAML 和代码，它们将创建一组绑定到“Product”表中的数据的控件****。 有关生成的 XAML 和代码的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

5. 在设计器中，单击“客户 ID”标签旁边的文本框****。

6. 在“属性”窗口，选中“IsReadOnly”属性旁边的复选框********。

7. 设置以下每个文本框的“IsReadOnly”属性****：

    - **采购订单号**

    - **销售订单 ID**

    - **Sales Order Number**

## <a name="load-the-data-from-the-service"></a>从服务中加载数据

使用服务代理对象从服务中加载销售数据。 然后，将返回的数据分配给 <xref:System.Windows.Data.CollectionViewSource> WPF 窗口中的数据源。

1. 在设计器创建`Window_Loaded`事件处理程序中，双击读取的文本：**MainWindow**

2. 将该事件处理程序替换为以下代码。 确保将此代码中的“localhost”地址替换为你的开发计算机上的本地主机地址**。

     [!code-csharp[Data_WPFWCF#2](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_2.cs)]
     [!code-vb[Data_WPFWCF#2](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_2.vb)]

## <a name="navigate-sales-records"></a>导航销售记录

添加使用户能够使用按钮滚动销售记录的代码 **\<** and **>** 。

1. 在设计器中，双击 **<** 窗口图面上的按钮。

     Visual Studio 打开代码隐藏文件，并为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件创建新的 `backButton_Click` 事件处理程序。

2. 将以下代码添加到生成的 `backButton_Click` 事件处理程序中：

     [!code-csharp[Data_WPFWCF#3](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_3.cs)]
     [!code-vb[Data_WPFWCF#3](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_3.vb)]

3. 返回到设计器，然后双击 **>** 按钮。

     Visual Studio 打开代码隐藏文件，并为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件创建新的 `nextButton_Click` 事件处理程序。

4. 将以下代码添加到生成的 `nextButton_Click` 事件处理程序中：

     [!code-csharp[Data_WPFWCF#4](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_4.cs)]
     [!code-vb[Data_WPFWCF#4](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_4.vb)]

## <a name="save-changes-to-sales-records"></a>保存对销售记录所做的更改

添加可让用户通过使用“保存更改”按钮来查看和保存对销售记录所做的更改的代码****：

1. 在设计器中，双击 "**保存更改**" 按钮。

     Visual Studio 打开代码隐藏文件，并为 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件创建新的 `saveButton_Click` 事件处理程序。

2. 将以下代码添加到 `saveButton_Click` 事件处理程序中。

     [!code-csharp[Data_WPFWCF#5](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_5.cs)]
     [!code-vb[Data_WPFWCF#5](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_5.vb)]

## <a name="test-the-application"></a>测试应用程序

生成并运行应用程序，以验证你是否可以查看和更新客户记录：

1. 在 "**生成**" 菜单上，单击 "**生成解决方案**"。 验证解决方案已生成且未发生错误。

2. 按**Ctrl** + **F5**。

     Visual Studio 启动“AdventureWorksService”项目，但不对其进行调试****。

3. 在“解决方案资源管理器”中，右键单击“AdventureWorksSalesEditor”项目********。

4. 在右击菜单（上下文菜单）上，在 "**调试**" 下，单击 "**启动新实例**"。

     将运行应用程序。 检查下列各项：

    - 文本框显示销售订单 ID 为“71774”的第一条销售记录中的数据的不同字段****。

    - 您可以单击 **>** 或 **<** 按钮以浏览其他销售记录。

5. 在某条销售记录中，在“注释”框中键入一些文本，然后单击“保存更改”********。

6. 关闭应用程序，然后从 Visual Studio 中再次启动该应用程序。

7. 导航到所更改的销售记录，然后验证相关更改是否在你关闭并重新打开应用程序后得以保留。

8. 关闭该应用程序。

## <a name="next-steps"></a>后续步骤

完成本演练后，你可以执行以下相关任务：

- 了解如何使用 Visual Studio 中的“数据源”窗口将 WPF 控件绑定到其他类型的数据源上****。 有关详细信息，请参阅[将 WPF 控件绑定到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)。

- 了解如何使用 Visual Studio 中的“数据源”窗口在 WPF 控件中显示相关数据（即父-子关系中的数据）****。 有关详细信息，请参阅[演练：在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [将 WPF 控件绑定到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)
- [WCF 概述（.NET Framework）](/dotnet/framework/data/wcf/wcf-data-services-overview)
- [实体框架概述（.NET Framework）](/dotnet/framework/data/adonet/ef/overview)
- [数据绑定概述（.NET Framework）](/dotnet/desktop-wpf/data/data-binding-overview)
