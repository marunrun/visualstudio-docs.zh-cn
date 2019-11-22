---
title: 'Walkthrough: Displaying Related Data in a WPF Application | Microsoft Docs'
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

In this walkthrough, you will create a WPF application that displays data from database tables that have a parent/child relationship. The data is encapsulated in entities in an Entity Data Model. The parent entity contains overview information for a set of orders. Each property of this entity is bound to a different control in the application. The child entity contains details for each order. This set of data is bound to a <xref:System.Windows.Controls.DataGrid> control.

 本演练阐释了以下任务：

- Creating a WPF application and an Entity Data Model that is generated from data in the AdventureWorksLT sample database.

- Creating a set of data-bound controls that display overview information for a set of orders. You create the controls by dragging a parent entity from the **Data Sources** window to **the WPF Designer**.

- Creating a <xref:System.Windows.Controls.DataGrid> control that displays related details for each selected order. You create the controls by dragging a child entity from the **Data Sources** window to a window in **the WPF designer**.

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Prerequisites
 你需要以下组件来完成本演练：

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]

- 对附加了 AdventureWorksLT 示例数据库的 SQL Server 或 SQL Server Express 的正在运行的实例的访问权限。 You can download the AdventureWorksLT database from the [CodePlex Web site](https://go.microsoft.com/fwlink/?linkid=87843).

  事先了解以下概念也很有用，但对于完成本演练并不是必需的：

- 实体数据模型和 ADO.NET 实体框架。 For more information, see [Entity Framework Overview](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0).

- 使用 WPF 设计器。 For more information, see [WPF and Silverlight Designer Overview](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62).

- WPF 数据绑定。 有关详细信息，请参阅 [数据绑定概述](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)。

## <a name="creating-the-project"></a>创建项目
 Create a new WPF project to display the order records.

#### <a name="to-create-a-new-wpf-project"></a>To create a new WPF project

1. 启动 Visual Studio。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

3. Expand **Visual C#** or **Visual Basic**, and then select **Windows**.

4. Make sure that **.NET Framework 4** is selected in the combo box at the top of the dialog box. The <xref:System.Windows.Controls.DataGrid> control that you use in this walkthrough is available only in the .NET Framework 4.

5. 选择“WPF 应用程序”项目模板。

6. 在“名称”框中键入 `AdventureWorksOrdersViewer`。

7. 单击“确定”。

     Visual Studio creates the `AdventureWorksOrdersViewer` project.

## <a name="creating-an-entity-data-model-for-the-application"></a>Creating an Entity Data Model for the Application
 必须先为应用程序定义数据模型并将此模型添加到“数据源”窗口中，然后才能创建数据绑定控件。 In this walkthrough, the data model is an Entity Data Model.

#### <a name="to-create-an-entity-data-model"></a>创建实体数据模型

1. On the **Data** menu, click **Add New Data Source** to open the **Data Source Configuration Wizard**.

2. On the **Choose a Data Source Type** page, click **Database**, and then click **Next**.

3. On the **Choose a Database Model** page, click **Entity Data Model**, and then click **Next**.

4. On the **Choose Model Contents** page, click **Generate from database**, and then click **Next**.

5. On the **Choose Your Data Connection** page, do one of the following:

   - 如果下拉列表中包含到 AdventureWorksLT 示例数据库的数据连接，请选择该连接。

      或

   - Click **New Connection** and create a connection to the AdventureWorksLT database.

     Make sure that the **Save entity connection settings in App.Config as** option is selected, and then click **Next**.

6. On the **Choose Your Database Objects** page, expand **Tables**, and then select the following tables:

   - **SalesOrderDetail**

   - **SalesOrderHeader**

7. 单击 **“完成”** 。

8. 生成项目。

## <a name="creating-data-bound-controls-that-display-the-orders"></a>Creating Data-Bound Controls that Display the Orders
 Create controls that display order records by dragging the `SalesOrderHeaders` entity from the **Data Sources** window to the WPF designer.

#### <a name="to-create-data-bound-controls-that-display-the-order-records"></a>To create data-bound controls that display the order records

1. In **Solution Explorer**, double-click MainWindow.xaml.

    将在 WPF 设计器中打开相应的窗口。

2. Edit the XAML so the **Height** and **Width** properties are set to 800

3. In the **Data Sources** window, click the drop-down menu for the **SalesOrderHeaders** node and select **Details**.

4. 展开“SalesOrderHeaders”节点。

5. Click the drop-down menu next to **SalesOrderID** and select **ComboBox**.

6. For each of the following child nodes of the **SalesOrderHeaders** node, click the drop-down menu next the node and select **None**:

   - **RevisionNumber**

   - **OnlineOrderFlag**

   - **ShipToAddressID**

   - **BillToAddressID**

   - **CreditCardApprovalCode**

   - **SubTotal**

   - **TaxAmt**

   - **Freight**

   - **rowguid**

   - **ModifiedDate**

     此操作将阻止 Visual Studio 在下一步中为这些节点创建数据绑定控件。 对于本演练，假定最终用户不需要查看此数据。

7. From the **Data Sources** window, drag the **SalesOrderHeaders** node to the window in **the WPF Designer**.

    Visual Studio generates XAML that creates a set of controls that are bound to data in the **SalesOrderHeaders** entity, and code that loads the data. For more information about the generated XAML and code, see [Bind WPF controls to data in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).

8. In the designer, click the combo box next to the **Sales Order ID** label.

9. 在“属性”窗口，选中“IsReadOnly”属性旁边的复选框。

## <a name="creating-a-datagrid-that-displays-the-order-details"></a>Creating a DataGrid that Displays the Order Details
 Create a <xref:System.Windows.Controls.DataGrid> control that displays order details by dragging the `SalesOrderDetails` entity from the **Data Sources** window to the WPF designer.

#### <a name="to-create-a-datagrid-that-displays-the-order-details"></a>To create a DataGrid that displays the order details

1. In the **Data Sources** window, locate the **SalesOrderDetails** node that is a child of the **SalesOrderHeaders** node.

   > [!NOTE]
   > There is also a **SalesOrderDetails** node that is a peer of the **SalesOrderHeaders** node. Make sure that you select the child node of the **SalesOrderHeaders** node.

2. Expand the child **SalesOrderDetails** node.

3. For each of the following child nodes of the **SalesOrderDetails** node, click the drop-down menu next the node and select **None**:

   - **SalesOrderID**

   - **SalesOrderDetailID**

   - **rowguid**

   - **ModifiedDate**

     This action prevents Visual Studio from including this data in the <xref:System.Windows.Controls.DataGrid> control you create in the next step. 对于本演练，假定最终用户不需要查看此数据。

4. From the **Data Sources** window, drag the child **SalesOrderDetails** node to the window in **the WPF Designer**.

    Visual Studio generates XAML to define a new data-bound <xref:System.Windows.Controls.DataGrid> control, and the control appears in the designer. Visual Studio also updates the generated `GetSalesOrderHeadersQuery` method in the code-behind file to include the data in the **SalesOrderDetails** entity.

## <a name="testing-the-application"></a>测试应用程序
 Build and run the application to verify that it displays the order records.

#### <a name="to-test-the-application"></a>测试应用程序

1. 按 F5。

     这将生成并运行应用程序。 验证以下内容：

    - The **Sales Order ID** combo box displays **71774**. This is the first order ID in the entity.

    - For each order you select in the **Sales Order ID** combo box, detailed order information is displayed in the <xref:System.Windows.Controls.DataGrid>.

2. 关闭该应用程序。

## <a name="next-steps"></a>后续步骤
 After completing this walkthrough, learn how to use the **Data Sources** window in Visual Studio to bind WPF controls to other types of data sources. For more information, see [Bind WPF controls to a WCF data service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md) and [Bind WPF controls to a dataset](../data-tools/bind-wpf-controls-to-a-dataset.md).

## <a name="see-also"></a>请参阅
 [Bind WPF controls to data in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md) [Display related data in WPF applications](../data-tools/display-related-data-in-wpf-applications.md)