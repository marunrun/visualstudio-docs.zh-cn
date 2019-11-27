---
title: 将 WPF 控件绑定到 WCF 数据服务 |Microsoft Docs
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
ms.assetid: 8823537c-82f0-41f7-bf30-705f0e5e59fd
caps.latest.revision: 44
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a3d1aab68e3dc9f33e0b3e9f9a5665d59f6f2ddc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299410"
---
# <a name="bind-wpf-controls-to-a-wcf-data-service"></a>将 WPF 控件绑定到 WCF 数据服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，你将创建一个包含数据绑定控件的 WPF 应用程序。 这些控件将绑定到在 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 中封装的客户记录。 你还将添加客户可用于查看和更新记录的按钮。

 本演练阐释了以下任务：

- 创建一个利用 AdventureWorksLT 示例数据库中的数据生成的实体数据模型。

- 创建 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)]，用于向 WPF 应用程序公开实体数据模型中的数据。

- 通过将项从“数据源”窗口拖到 WPF 设计器来创建一组数据绑定控件。

- 创建用于向前/向后导航客户记录的按钮。

- 创建一个按钮，用于将对控件中的数据所做的更改保存到 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 和基础数据源。

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 你需要以下组件来完成本演练：

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]

- 对附加了 AdventureWorksLT 示例数据库的 SQL Server 或 SQL Server Express 的正在运行的实例的访问权限。 可以从[CodePlex](https://go.microsoft.com/fwlink/?linkid=87843)网站下载 AdventureWorksLT 数据库。

  事先了解以下概念也很有用，但对于完成本演练并不是必需的：

- WCF 数据服务。 有关详细信息，请参阅[概述](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb)。

- [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] 中的数据模型。

- 实体数据模型和 ADO.NET 实体框架。 有关详细信息，请参阅[实体框架概述](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0)。

- 使用 WPF 设计器。 有关详细信息，请参阅[WPF 和 Silverlight 设计器概述](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)。

- WPF 数据绑定。 有关详细信息，请参阅 [数据绑定概述](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)。

## <a name="create-the-service-project"></a>创建服务项目
 从为 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 创建项目开始本演练。

#### <a name="to-create-the-service-project"></a>创建服务项目

1. 启动 Visual Studio。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

3. 展开“Visual C#”或“Visual Basic”，然后选择“Web”。

4. 选择“ASP.NET Web 应用程序”项目模板。

5. 在 "**名称**" 框中，键入 `AdventureWorksService` 然后单击 **"确定"** 。

     Visual Studio 将创建 `AdventureWorksService` 项目。

6. 在“解决方案资源管理器”中，右键单击“Default.aspx”，然后选择“删除”。 本演练中不需要此文件。

## <a name="create-an-entity-data-model-for-the-service"></a>为服务创建实体数据模型
 若要通过使用 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 向应用程序公开数据，则必须为该服务定义一个数据模型。 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 支持两种类型的数据模型：实体数据模型和使用实现 <xref:System.Linq.IQueryable%601> 接口的公共语言运行时（CLR）对象定义的自定义数据模型。 在本演练中，你将为该数据模型创建一个实体数据模型。

#### <a name="to-create-an-entity-data-model"></a>创建实体数据模型

1. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

2. 在“已安装的模板”列表中，单击“数据”，然后选择“ADO.NET 实体数据模型”项目项。

3. 将名称更改为 "`AdventureWorksModel.edmx`"，然后单击 "**添加**"。

     “实体数据模型”向导随即打开。

4. 在“选择模型内容”页面上，单击“从数据库生成”，然后单击“下一步”。

5. 在“选择你的数据连接”页面上，选择以下选项之一：

    - 如果下拉列表中包含到 AdventureWorksLT 示例数据库的数据连接，请选择该连接。

    - 单击“新建连接”，然后创建到 AdventureWorksLT 数据库的连接。

6. 在“选择数据连接”页面上，确保选中了“将 App.Config 中的实体连接设置另存为”选项，然后单击“下一步”。

7. 在“选择数据库对象”页面上，展开“表”，然后选择“SalesOrderHeader”表。

8. 单击 **“完成”** 。

## <a name="create-the-service"></a>创建服务
 创建 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 以向 WPF 应用程序公开实体数据模型中的数据。

#### <a name="to-create-the-service"></a>创建服务

1. 在“项目”菜单上，选择“添加新项”。

2. 在 "已安装的模板" 列表中，单击 " **Web**"，然后选择 " **WCF 数据服务**" 项目项。

3. 在 "**名称**" 框中，键入 `AdventureWorksService.svc`，然后单击 "**添加**"。

     Visual Studio 将 `AdventureWorksService.svc` 添加到项目。

## <a name="configure-the-service"></a>配置服务
 必须配置该服务，才能操作所创建的实体数据模型。

#### <a name="to-configure-the-service"></a>配置服务

1. 在 `AdventureWorks.svc` 代码文件中，将 `AdventureWorksService` 类声明替换为以下代码。

     [!code-csharp[Data_WPFWCF#1](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworksservice.svc.cs#1)]
     [!code-vb[Data_WPFWCF#1](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworksservice.svc.vb#1)]

     此代码将更新 `AdventureWorksService` 类，使其派生自对实体数据模型中的 `AdventureWorksLTEntities` 对象上下文类进行操作的 <xref:System.Data.Services.DataService%601>。 此代码还将更新 `InitializeService` 方法，以使服务的客户端具有对 `SalesOrderHeader` 实体的完全读/写访问权限。

2. 生成项目，并确认生成过程中未发生错误。

## <a name="create-the-wpf-client-application"></a>创建 WPF 客户端应用程序
 若要显示 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 中的数据，请使用基于该服务的数据源创建一个新的 WPF 应用程序。 在本演练后面的部分中，你将向该应用程序中添加数据绑定控件。

#### <a name="to-create-the-wpf-client-application"></a>创建 WPF 客户端应用程序

1. 在“解决方案资源管理器”中，右键单击解决方案节点、单击“添加”，然后选择“新建项目”。

2. 在“新建项目”对话框中，展开“Visual C#”或“Visual Basic”，然后选择“Windows”。

3. 选择“WPF 应用程序”项目模板。

4. 在“名称”框中，键入 **，然后单击“确定”。** `AdventureWorksSalesEditor`

     Visual Studio 会将 `AdventureWorksSalesEditor` 项目添加到解决方案中。

5. 在 **“数据”** 菜单上，单击 **“显示数据源”** 。

     “数据源”窗口随即打开。

6. 在 **“数据源”** 窗口中，单击 **“添加新数据源”** 。

     “数据源配置”向导随即打开。

7. 在该向导的“选择数据源类型”页面上，选择“服务”，然后单击“下一步”。

8. 在“添加服务引用”对话框中，单击“发现”。

     Visual Studio 会在当前解决方案中搜索可用服务，并将 `AdventureWorksService.svc` 添加到 "**服务**" 框中的可用服务列表。

9. 在 "**命名空间**" 框中，键入 `AdventureWorksService`。

10. 在“服务”框中，单击“AdventureWorksService.svc”，然后单击“确定”。

     Visual Studio 将下载服务信息，然后返回到 "**数据源配置**向导"。

11. 在“添加服务引用”页面上，单击“完成”。

     Visual Studio 会将表示该服务返回的数据的节点添加到“数据源”窗口中。

## <a name="define-the-user-interface-of-the-window"></a>定义窗口的用户界面
 通过在 WPF 设计器中修改 XAML，将多个按钮添加到该窗口中。 在本演练后面的部分中，你将添加可让用户通过使用这些按钮来查看和更新销售记录的代码。

#### <a name="to-create-the-window-layout"></a>创建窗口布局

1. 在**解决方案资源管理器**中，双击 "mainwindow.xaml"。

     将在 WPF 设计器中打开相应的窗口。

2. 在设计器的 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 视图中，在 `<Grid>` 标记之间添加以下代码：

    ```
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
 通过将 "`SalesOrderHeaders`" 节点从 "**数据源**" 窗口拖到设计器，创建显示客户记录的控件。

#### <a name="to-create-the-data-bound-controls"></a>创建数据绑定控件

1. 在“数据源”窗口中，单击“SalesOrderHeaders”节点的下拉菜单，然后选择“详细信息”。

2. 展开“SalesOrderHeaders”节点。

3. 在本示例中，某些字段不会显示，因此只需单击下列节点旁边的下拉菜单，然后选择“无”：

   - **CreditCardApprovalCode**

   - **ModifiedDate**

   - **OnlineOrderFlag**

   - **RevisionNumber**

   - **rowguid**

     此操作将阻止 Visual Studio 在下一步中为这些节点创建数据绑定控件。 对于本演练，假设最终用户不需要查看此数据。

4. 从“数据源”窗口中，将“SalesOrderHeaders”节点拖到包含按钮的行的下方的网格行。

    Visual Studio 将生成 XAML 和代码，它们将创建一组绑定到“Product”表中的数据的控件。 有关生成的 XAML 和代码的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

5. 在设计器中，单击“客户 ID”标签旁边的文本框。

6. 在“属性”窗口，选中“IsReadOnly”属性旁边的复选框。

7. 设置以下每个文本框的“IsReadOnly”属性：

   - **采购订单号**

   - **销售订单 ID**

   - **销售订单号**

## <a name="load-the-data-from-the-service"></a>从服务中加载数据
 使用服务代理对象从服务中加载销售数据。 然后，将返回的数据分配给 WPF 窗口中 <xref:System.Windows.Data.CollectionViewSource> 的数据源。

#### <a name="to-load-the-data-from-the-service"></a>从服务中加载数据

1. 在设计器创建`Window_Loaded`事件处理程序中，双击读取的文本：**MainWindow**

2. 将该事件处理程序替换为以下代码。 确保将此代码中的“localhost”地址替换为你的开发计算机上的本地主机地址。

     [!code-csharp[Data_WPFWCF#2](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#2)]
     [!code-vb[Data_WPFWCF#2](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#2)]

## <a name="navigatesales-records"></a>Navigatesales 记录
 添加可让用户通过“ **”和“\<”按钮来滚动销售记录的代码** **>** 。

#### <a name="to-enable-users-to-navigate-sales-records"></a>使用户能够导航销售记录

1. 在设计器中，双击窗口窗面上的“ **”按钮<** 。

     Visual Studio 打开代码隐藏文件，并为 `backButton_Click` 事件创建新的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序。

2. 将以下代码添加到生成的 `backButton_Click` 事件处理程序中：

     [!code-csharp[Data_WPFWCF#3](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#3)]
     [!code-vb[Data_WPFWCF#3](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#3)]

3. 返回到设计器，然后双击“ **”按钮>** 。

     Visual Studio 打开代码隐藏文件，并为 `nextButton_Click` 事件创建新的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序。

4. 将以下代码添加到生成的 `nextButton_Click` 事件处理程序中：

     [!code-csharp[Data_WPFWCF#4](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#4)]
     [!code-vb[Data_WPFWCF#4](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#4)]

## <a name="saving-changes-to-sales-records"></a>保存对销售记录所做的更改
 添加可让用户通过使用 "**保存更改**" 按钮来查看和保存对销售记录所做更改的代码。

#### <a name="to-add-the-ability-to-save-changes-to-sales-records"></a>添加保存对销售记录所做更改的功能

1. 在设计器中，双击“保存更改”按钮。

     Visual Studio 打开代码隐藏文件，并为 `saveButton_Click` 事件创建新的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序。

2. 将以下代码添加到 `saveButton_Click` 事件处理程序中。

     [!code-csharp[Data_WPFWCF#5](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#5)]
     [!code-vb[Data_WPFWCF#5](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#5)]

## <a name="testing-the-application"></a>测试应用程序
 生成并运行应用程序，以验证你是否可以查看和更新客户记录。

#### <a name="to-test-the-application"></a>测试应用程序

1. 在 "**生成**" 菜单上，单击 "**生成解决方案**"。 验证解决方案已生成且未发生错误。

2. 按**Ctrl + F5**。

     Visual Studio 启动“AdventureWorksService”项目，但不对其进行调试。

3. 在“解决方案资源管理器”中，右键单击“AdventureWorksSalesEditor”项目。

4. 在上下文菜单上的“调试”下，单击“启动新实例”。

     将运行应用程序。 验证以下内容：

    - 文本框显示销售订单 ID 为“71774”的第一条销售记录中的数据的不同字段。

    - 可以单击“ **”或“>”按钮来导航其他销售记录** **<** 。

5. 在某条销售记录中，在“注释”框中键入一些文本，然后单击“保存更改”。

6. 关闭应用程序，然后从 Visual Studio 中再次启动该应用程序。

7. 导航到所更改的销售记录，然后验证相关更改是否在你关闭并重新打开应用程序后得以保留。

8. 关闭该应用程序。

## <a name="next-steps"></a>后续步骤
 完成本演练后，你可以执行以下相关任务：

- 了解如何使用 Visual Studio 中的“数据源”窗口将 WPF 控件绑定到其他类型的数据源上。 有关详细信息，请参阅[将 WPF 控件绑定到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)。

- 了解如何使用 Visual Studio 中的“数据源”窗口在 WPF 控件中显示相关数据（即父-子关系中的数据）。 有关详细信息，请参阅[演练：在 WPF 应用程序中显示相关数据](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)。

## <a name="see-also"></a>请参阅
 [将 wpf 控件绑定到 Visual studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)将 wpf 控件绑定到[visual studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md)将 wpf 控件绑定到数据[集](../data-tools/bind-wpf-controls-to-a-dataset.md)[概述](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb)[实体框架概述](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0) [wpf 和 Silverlight 设计器概述](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)[数据绑定概述](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)
