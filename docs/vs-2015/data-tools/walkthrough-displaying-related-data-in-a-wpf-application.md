---
title: 演练：在 WPF 应用程序中显示相关数据 |Microsoft Docs
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
ms.assetid: 5c48f188-e9c4-40a6-97d9-67cdb2f90127
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 787be52eeb546d2ab184a172464862d10cb43288
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299584"
---
# <a name="walkthrough-displaying-related-data-in-a-wpf-application"></a>演练：在 WPF 应用程序中显示相关数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，您将创建一个 WPF 应用程序，用于显示具有父/子关系的数据库表中的数据。 数据封装在实体数据模型中的实体内。 父实体包含一组订单的概述信息。 此实体的每个属性都绑定到应用程序中的另一个控件。 子实体包含每个订单的详细信息。 此数据集绑定到 <xref:System.Windows.Controls.DataGrid> 控件。

 本演练阐释了以下任务：

- 创建从 AdventureWorksLT 示例数据库中的数据生成的 WPF 应用程序和实体数据模型。

- 创建一组数据绑定控件，这些控件显示一组订单的概述信息。 通过将父实体从 "**数据源**" 窗口拖到**WPF 设计器**来创建控件。

- 创建一个 <xref:System.Windows.Controls.DataGrid> 控件，该控件显示每个所选订单的相关详细信息。 您可以通过将子实体从 "**数据源**" 窗口拖到**WPF 设计器**中的窗口来创建控件。

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 你需要以下组件来完成本演练：

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

- 对附加了 AdventureWorksLT 示例数据库的 SQL Server 或 SQL Server Express 的正在运行的实例的访问权限。 可以从[CodePlex](https://go.microsoft.com/fwlink/?linkid=87843)网站下载 AdventureWorksLT 数据库。

  事先了解以下概念也很有用，但对于完成本演练并不是必需的：

- 实体数据模型和 ADO.NET 实体框架。 有关详细信息，请参阅[实体框架概述](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0)。

- 使用 WPF 设计器。 有关详细信息，请参阅[WPF 和 Silverlight 设计器概述](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)。

- WPF 数据绑定。 有关详细信息，请参阅 [数据绑定概述](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)。

## <a name="creating-the-project"></a>创建项目
 创建新的 WPF 项目以显示订单记录。

#### <a name="to-create-a-new-wpf-project"></a>创建新的 WPF 项目

1. 启动 Visual Studio。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

3. 展开 **" C#视觉对象**" 或 " **Visual Basic**"，然后选择 " **Windows**"。

4. 请确保在对话框顶部的组合框中选择了 " **.NET Framework 4** "。 本演练中使用的 <xref:System.Windows.Controls.DataGrid> 控件仅在 .NET Framework 4 中可用。

5. 选择“WPF 应用程序”项目模板。

6. 在“名称”框中键入 `AdventureWorksOrdersViewer`。

7. 单击" **确定**"。

     Visual Studio 将创建 `AdventureWorksOrdersViewer` 项目。

## <a name="creating-an-entity-data-model-for-the-application"></a>为应用程序创建实体数据模型
 必须先为应用程序定义数据模型并将此模型添加到“数据源”窗口中，然后才能创建数据绑定控件。 在本演练中，数据模型是实体数据模型。

#### <a name="to-create-an-entity-data-model"></a>创建实体数据模型

1. 在 "**数据**" 菜单上，单击 "**添加新数据源**" 以打开 "**数据源配置向导**"。

2. 在 "**选择数据源类型**" 页上，单击 "**数据库**"，然后单击 "**下一步**"。

3. 在 "**选择数据库模型**" 页上，单击 "**实体数据模型**"，然后单击 "**下一步**"。

4. 在 "**选择模型内容**" 页上，单击 "**从数据库生成**"，然后单击 "**下一步**"。

5. 在 "**选择你的数据连接**" 页上，执行下列操作之一：

   - 如果下拉列表中包含到 AdventureWorksLT 示例数据库的数据连接，请选择该连接。

      或

   - 单击 "**新建连接**"，并创建与 AdventureWorksLT 数据库的连接。

     确保选中 "将 app.config**中的实体连接设置另存为**" 选项，然后单击 "**下一步**"。

6. 在 "**选择数据库对象**" 页上，展开 "**表**"，然后选择以下表：

   - **SalesOrderDetail**

   - **SalesOrderHeader**

7. 单击 **“完成”** 。

8. 生成项目。

## <a name="creating-data-bound-controls-that-display-the-orders"></a>创建显示订单的数据绑定控件
 通过将 `SalesOrderHeaders` 实体从 "**数据源**" 窗口拖到 WPF 设计器来创建显示订单记录的控件。

#### <a name="to-create-data-bound-controls-that-display-the-order-records"></a>创建显示订单记录的数据绑定控件

1. 在**解决方案资源管理器**中，双击 "mainwindow.xaml"。

    将在 WPF 设计器中打开相应的窗口。

2. 编辑 XAML，使 "**高度**" 和 "**宽度**" 属性设置为800

3. 在 "**数据源**" 窗口中，单击 " **SalesOrderHeaders** " 节点的下拉菜单，然后选择 "**详细信息**"。

4. 展开“SalesOrderHeaders”节点。

5. 单击 " **SalesOrderID** " 旁边的下拉菜单，然后选择 " **ComboBox**"。

6. 对于**SalesOrderHeaders**节点的以下每个子节点，单击节点旁边的下拉菜单，并选择 "**无**"：

   - **RevisionNumber**

   - **OnlineOrderFlag**

   - **ShipToAddressID**

   - **BillToAddressID**

   - **CreditCardApprovalCode**

   - **进行**

   - **TaxAmt**

   - **代理**

   - **rowguid**

   - **ModifiedDate**

     此操作将阻止 Visual Studio 在下一步中为这些节点创建数据绑定控件。 对于本演练，假定最终用户不需要查看此数据。

7. 从 "**数据源**" 窗口中，将 " **SalesOrderHeaders** " 节点拖至**WPF 设计器**中的窗口。

    Visual Studio 将生成用于创建一组控件的 XAML，这些控件绑定到**SalesOrderHeaders**实体中的数据以及用于加载数据的代码。 有关生成的 XAML 和代码的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

8. 在设计器中，单击 "**销售订单 ID** " 标签旁边的组合框。

9. 在“属性”窗口，选中“IsReadOnly”属性旁边的复选框。

## <a name="creating-a-datagrid-that-displays-the-order-details"></a>创建显示订单详细信息的 DataGrid
 通过将 `SalesOrderDetails` 实体从 "**数据源**" 窗口拖到 WPF 设计器来创建显示订单详细信息的 <xref:System.Windows.Controls.DataGrid> 控件。

#### <a name="to-create-a-datagrid-that-displays-the-order-details"></a>创建显示订单详细信息的 DataGrid

1. 在 "**数据源**" 窗口中，找到作为 " **SalesOrderHeaders** " 节点的子节点的 " **SalesOrderDetails** " 节点。

   > [!NOTE]
   > 还有一个**SalesOrderDetails**节点，它是**SalesOrderHeaders**节点的对等节点。 请确保选择 " **SalesOrderHeaders** " 节点的子节点。

2. 展开 "子**SalesOrderDetails** " 节点。

3. 对于**SalesOrderDetails**节点的以下每个子节点，单击节点旁边的下拉菜单，并选择 "**无**"：

   - **SalesOrderID**

   - **SalesOrderDetailID**

   - **rowguid**

   - **ModifiedDate**

     此操作可防止 Visual Studio 将此数据包含在下一步中创建的 <xref:System.Windows.Controls.DataGrid> 控件中。 对于本演练，假定最终用户不需要查看此数据。

4. 从 "**数据源**" 窗口中，将子**SalesOrderDetails**节点拖至**WPF 设计器**中的窗口。

    Visual Studio 将生成 XAML 来定义新的数据绑定 <xref:System.Windows.Controls.DataGrid> 控件，并在设计器中显示该控件。 Visual Studio 还会更新代码隐藏文件中生成的 `GetSalesOrderHeadersQuery` 方法，以便在**SalesOrderDetails**实体中包含数据。

## <a name="testing-the-application"></a>测试应用程序
 生成并运行应用程序以验证其是否显示订单记录。

#### <a name="to-test-the-application"></a>测试应用程序

1. 按 F5。

     这将生成并运行应用程序。 验证以下内容：

    - "**销售订单 ID** " 组合框显示**71774**。 这是实体中的第一个订单 ID。

    - 对于在 "**销售订单 ID** " 组合框中选择的每个订单，详细订单信息将显示在 "<xref:System.Windows.Controls.DataGrid>中。

2. 关闭该应用程序。

## <a name="next-steps"></a>后续步骤
 完成本演练后，了解如何使用 Visual Studio 中的 "**数据源**" 窗口将 WPF 控件绑定到其他类型的数据源。 有关详细信息，请参阅[将 wpf 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)和将[wpf 控件绑定到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)。

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中将 wpf 控件绑定到数据在](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md) [wpf 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)