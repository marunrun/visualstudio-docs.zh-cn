---
title: 演练：在 WPF 应用程序中显示相关的数据 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 560852fc25a3e00134e4ed8b6bd06205248b208d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65688426"
---
# <a name="walkthrough-displaying-related-data-in-a-wpf-application"></a>演练：在 WPF 应用程序中显示相关的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，将创建显示具有父/子关系的数据库表中的数据的 WPF 应用程序。 将数据封装在实体数据模型中的实体。 父实体包含一组的订单的概述信息。 此实体的每个属性绑定到一个不同的应用程序中的控件。 子实体包含每个订单的详细信息。 此数据集绑定到<xref:System.Windows.Controls.DataGrid>控件。  
  
 本演练阐释了以下任务：  
  
- 创建 WPF 应用程序和实体数据模型的 AdventureWorksLT 示例数据库中的数据生成的。  
  
- 创建一组数据绑定控件显示订单的一组的概述信息。 通过将父实体从创建控件**数据源**到窗口**WPF 设计器**。  
  
- 创建<xref:System.Windows.Controls.DataGrid>选择顺序显示每个相关的详细信息的控件。 通过将子实体从创建控件**数据源**窗口中的一个窗口**WPF 设计器**。  
  
   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>系统必备  
 你需要以下组件来完成本演练：  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
- 对附加了 AdventureWorksLT 示例数据库的 SQL Server 或 SQL Server Express 的正在运行的实例的访问权限。 您可以下载 AdventureWorksLT 数据库从[CodePlex 网站上](http://go.microsoft.com/fwlink/?linkid=87843)。  
  
  事先了解以下概念也很有用，但对于完成本演练并不是必需的：  
  
- 实体数据模型和 ADO.NET 实体框架。 有关详细信息，请参阅[实体框架概述](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0)。  
  
- 使用 WPF 设计器。 有关详细信息，请参阅[WPF 和 Silverlight 设计器概述](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)。  
  
- WPF 数据绑定。 有关详细信息，请参阅[数据绑定概述](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)。  
  
## <a name="creating-the-project"></a>创建项目  
 创建新的 WPF 项目以显示订单记录。  
  
#### <a name="to-create-a-new-wpf-project"></a>若要创建新的 WPF 项目  
  
1. 启动 Visual Studio。  
  
2. 在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
3. 展开**Visual C#** 或**Visual Basic**，然后选择**Windows**。  
  
4. 请确保 **.NET Framework 4**选择对话框顶部组合框中。 <xref:System.Windows.Controls.DataGrid>在本演练中使用的控件是仅在.NET Framework 4 中可用。  
  
5. 选择“WPF 应用程序”项目模板。  
  
6. 在“名称”框中键入 `AdventureWorksOrdersViewer`。  
  
7. 单击 **“确定”**。  
  
     Visual Studio 将创建`AdventureWorksOrdersViewer`项目。  
  
## <a name="creating-an-entity-data-model-for-the-application"></a>为应用程序创建实体数据模型  
 必须先为应用程序定义数据模型并将此模型添加到“数据源”窗口中，然后才能创建数据绑定控件。 在此演练中，数据模型是实体数据模型。  
  
#### <a name="to-create-an-entity-data-model"></a>创建实体数据模型  
  
1. 上**数据**菜单上，单击**添加新数据源**以打开**数据源配置向导**。  
  
2. 上**选择数据源类型**页上，单击**数据库**，然后单击**下一步**。  
  
3. 上**选择数据库模型**页上，单击**实体数据模型**，然后单击**下一步**。  
  
4. 上**选择模型内容**页上，单击**从数据库生成**，然后单击**下一步**。  
  
5. 上**选择数据连接**页上，执行下列操作之一：  
  
   - 如果下拉列表中包含到 AdventureWorksLT 示例数据库的数据连接，请选择该连接。  
  
      或  
  
   - 单击**新的连接**并创建与 AdventureWorksLT 数据库的连接。  
  
     请确保**将实体连接设置保存在 App.Config 作为**选项选择后，然后依次**下一步**。  
  
6. 上**选择数据库对象**页上，展开**表**，，然后选择以下表：  
  
   - **SalesOrderDetail**  
  
   - **SalesOrderHeader**  
  
7. 单击 **“完成”**。  
  
8. 生成项目。  
  
## <a name="creating-data-bound-controls-that-display-the-orders"></a>创建数据绑定控件显示订单的  
 创建通过拖动显示订单记录的控件`SalesOrderHeaders`从实体**数据源**到 WPF 设计器窗口。  
  
#### <a name="to-create-data-bound-controls-that-display-the-order-records"></a>若要创建显示订单记录的数据绑定控件  
  
1. 在中**解决方案资源管理器**，双击 MainWindow.xaml。  
  
    将在 WPF 设计器中打开相应的窗口。  
  
2. 编辑 XAML，因此**高度**并**宽度**属性设置为 800  
  
3. 在中**数据源**窗口中，单击下拉列表菜单**SalesOrderHeaders**节点，然后选择**详细信息**。  
  
4. 展开“SalesOrderHeaders”节点。  
  
5. 单击下拉列表菜单旁边**SalesOrderID** ，然后选择**组合框**。  
  
6. 以下子节点的每个**SalesOrderHeaders**节点，单击下拉列表菜单，接下来的节点，然后选择**None**:  
  
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
  
7. 从**数据源**窗口中，拖动**SalesOrderHeaders**节点中的窗口**WPF 设计器**。  
  
    Visual Studio 将生成创建一组中的数据绑定控件的 XAML **SalesOrderHeaders**实体，并将数据加载的代码。 有关生成的 XAML 和代码的详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。  
  
8. 在设计器中，单击组合框旁边**销售订单 ID**标签。  
  
9. 在“属性”窗口，选中“IsReadOnly”属性旁边的复选框。  
  
## <a name="creating-a-datagrid-that-displays-the-order-details"></a>创建一个 DataGrid 显示订单详细信息  
 创建<xref:System.Windows.Controls.DataGrid>控件，用于显示订单详细信息，通过拖动`SalesOrderDetails`从实体**数据源**到 WPF 设计器窗口。  
  
#### <a name="to-create-a-datagrid-that-displays-the-order-details"></a>若要创建显示订单详细信息的 DataGrid  
  
1. 在中**数据源**窗口中，找到**SalesOrderDetails**节点的子级**SalesOrderHeaders**节点。  
  
   > [!NOTE]
   > 此外，还有**SalesOrderDetails**的对等节点**SalesOrderHeaders**节点。 请确保选择的子节点**SalesOrderHeaders**节点。  
  
2. 展开子**SalesOrderDetails**节点。  
  
3. 以下子节点的每个**SalesOrderDetails**节点，单击下拉列表菜单，接下来的节点，然后选择**None**:  
  
   - **SalesOrderID**  
  
   - **SalesOrderDetailID**  
  
   - **rowguid**  
  
   - **ModifiedDate**  
  
     此操作可防止 Visual Studio 中的此数据包括<xref:System.Windows.Controls.DataGrid>下一步中创建的控件。 对于本演练，假定最终用户不需要查看此数据。  
  
4. 从**数据源**窗口中，将子**SalesOrderDetails**节点中的窗口**WPF 设计器**。  
  
    Visual Studio 将生成 XAML 来定义新的数据绑定<xref:System.Windows.Controls.DataGrid>控件，且该控件将显示在设计器中。 Visual Studio 还会更新生成`GetSalesOrderHeadersQuery`要包括中的数据的代码隐藏文件中的方法**SalesOrderDetails**实体。  
  
## <a name="testing-the-application"></a>测试应用程序  
 生成并运行应用程序以验证它显示订单记录。  
  
#### <a name="to-test-the-application"></a>测试应用程序  
  
1. 按 F5 。  
  
     这将生成并运行应用程序。 验证以下内容：  
  
    - **销售订单 ID**组合框显示**71774**。 这是实体中的第一个订单 ID。  
  
    - 在中选择每个订单**销售订单 ID**组合框中显示详细的订单信息<xref:System.Windows.Controls.DataGrid>。  
  
2. 关闭该应用程序。  
  
## <a name="next-steps"></a>后续步骤  
 完成此演练后，了解如何使用**数据源**窗口在 Visual Studio 中将 WPF 控件添加到其他类型的数据源。 有关详细信息，请参阅[绑定 WPF 控件添加到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)并[绑定 WPF 控件添加到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)。  
  
## <a name="see-also"></a>请参阅  
 [将 WPF 控件绑定到 Visual Studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)   
 [在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)