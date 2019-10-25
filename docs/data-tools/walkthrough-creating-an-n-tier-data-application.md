---
title: 演练：创建 N 层数据应用程序
ms.date: 09/08/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, creating
- n-tier applications, walkthroughs
ms.assetid: d15e4d31-2839-48d9-9e0e-2e73404d82a2
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 8fad79423465ac3d90c426862f93f09d721c7df3
ms.sourcegitcommit: 8589d85cc10710ef87e6363a2effa5ee5610d46a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72806985"
---
# <a name="walkthrough-create-an-n-tier-data-application"></a>演练：创建 n 层数据应用程序
“N 层”数据应用程序是指用于访问数据且分为多个逻辑层（或“多层”）的应用程序。 通过将应用程序组件分离到相对独立的层中，可以提高应用程序的可维护性和可伸缩性。 该结构之所以具有这种优点，是因为它有利于采用可应用于单个层而无需重新设计整个解决方案的新技术。 N 层体系结构包括一个表示层、一个中间层和一个数据层。 中间层通常包括数据访问层、业务逻辑层和共享组件（例如身份验证和验证）。 数据层则包括关系数据库。 N 层应用程序通常将敏感信息存储在中间层的数据访问层中，目的是将它们与访问表示层的最终用户隔离。 有关详细信息，请参阅[N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)。

在 N 层应用程序中，分离各层的一种方法是为要包括在应用程序中的每一层创建相互独立的项目。 类型化数据集包含一个 `DataSet Project` 属性，该属性决定了生成的数据集和 `TableAdapter` 代码应归属到哪些项目中。

本演练演示如何使用“数据集设计器”将数据集和 `TableAdapter` 代码分离到相互独立的类库项目中。 分离数据集和 TableAdapter 代码后，将[在 Visual Studio 服务中创建 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)，以调入数据访问层。 最后，将 Windows 窗体应用程序创建为表示层。 该层将访问数据服务中的数据。

在本演练中，你将执行以下步骤：

- 创建一个新的包含多个项目的 n 层解决方案。

- 将两个类库项目添加到 N 层解决方案中。

- 使用“数据源配置”向导创建类型化数据集。

- 将生成的[tableadapter](create-and-configure-tableadapters.md)和数据集代码分离到不同的项目中。

- 创建 Windows Communication Foundation (WCF) 服务以调入数据访问层。

- 在服务中创建函数以从数据访问层检索数据。

- 创建 Windows 窗体应用程序来充当表示层。

- 创建绑定到数据源的 Windows 窗体控件。

- 编写代码以填充数据表。

![视频链接](../data-tools/media/playvideo.gif)本主题的视频版本，请参阅[视频帮助：创建 N 层数据应用程序](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/cc178916(v=vs.90))。

## <a name="prerequisites"></a>Prerequisites
本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果没有 SQL Server Express 的 LocalDB，请从[SQL Server Express 下载 "页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过**Visual Studio 安装程序**安装它。 在**Visual Studio 安装程序**中，可以将 SQL Server Express LocalDB 作为 **.net 桌面开发**工作负荷的一部分进行安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 " **SQL Server 对象资源管理器**" 窗口。 （**SQL Server 对象资源管理器**作为 Visual Studio 安装程序中的**数据存储和处理**工作负荷的一部分安装。）展开 " **SQL Server** " 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    2. 将[Northwind transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-sql 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    3. 将 T-sql 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询将完成运行，并创建 Northwind 数据库。

## <a name="create-the-n-tier-solution-and-class-library-to-hold-the-dataset-dataentitytier"></a>创建 n 层解决方案和类库以保存数据集（DataEntityTier）
本演练的第一步是创建一个解决方案和两个类库项目。 第一个类库包含数据集（生成的类型化 `DataSet` 类和保存应用程序数据的数据表）。 此项目将用作应用程序的数据实体层，它通常位于中间层内。 数据集创建初始数据集，并自动将代码分隔到两个类库中。

> [!NOTE]
> 请确保已正确命名项目和解决方案，然后再单击“确定”。 这样做可使你更轻松地完成本演练。

### <a name="to-create-the-n-tier-solution-and-dataentitytier-class-library"></a>创建 N 层解决方案和 DataEntityTier 类库

1. 在 Visual Studio 的 "**文件**" 菜单上，选择 "**新建** > **项目**"。

2. 在左侧窗格中展开 "**视觉对象C#**  " 或 " **Visual Basic** "，然后选择 " **Windows 桌面**"。

3. 在中间窗格中，选择 "**类库" 项目类型**。

4. 将项目命名为“DataEntityTier”。

5. 将解决方案命名为 " **NTierWalkthrough**"，然后选择 **"确定"** 。

     创建包含 DataEntityTier 项目的 NTierWalkthrough 解决方案并将其添加到“解决方案资源管理器”中。

## <a name="create-the-class-library-to-hold-the-tableadapters-dataaccesstier"></a>创建用于保存 Tableadapter 的类库（DataAccessTier）
创建 DataEntityTier 项目后，下一步是创建另一个类库项目。 此项目包含生成的 Tableadapter，称为应用程序的*数据访问层*。 数据访问层包含连接到数据库所需的信息，通常位于中间层内。

### <a name="to-create-a-separate-class-library-for-the-tableadapters"></a>为 Tableadapter 创建单独的类库

1. 右键单击“解决方案资源管理器”中的解决方案，然后选择“添加” > “新建项目”。

2. 在 "**新建项目**" 对话框中，在中间窗格**中选择 "类库"** 。

3. 将项目命名为**DataAccessTier** ，然后选择 **"确定"** 。

     DataAccessTier 项目即被创建并添加到 NTierWalkthrough 解决方案中。

## <a name="create-the-dataset"></a>创建数据集
下一步是创建类型化数据集。 类型化数据集是通过 dataset 类（包括 `DataTables` 类）和单个项目中的 `TableAdapter` 类创建的。 （所有类都生成到一个文件中。）将数据集和 Tableadapter 分隔到不同的项目中时，该数据集类将移动到另一个项目，并将 `TableAdapter` 类保留在原始项目中。 因此，在项目中创建将最终包含 Tableadapter （DataAccessTier 项目）的数据集。 您可以使用 "**数据源配置向导**" 创建数据集。

> [!NOTE]
> 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关如何设置 Northwind 示例数据库的信息，请参阅[如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

### <a name="to-create-the-dataset"></a>创建数据集

1. 在**解决方案资源管理器**中选择 " **DataAccessTier** "。

2. 在 "**数据**" 菜单上，选择 "**显示数据源**"。

   “数据源”窗口随即打开。

3. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

4. 在 "**选择数据源类型**" 页上，选择 "**数据库**"，然后选择 "**下一步**"。

5. 在“选择数据连接”页面上，执行以下操作之一：

     如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

     或

     选择 "**新建连接**" 以打开 "**添加连接**" 对话框。

6. 如果数据库需要密码，请选择该选项以包括敏感数据，然后选择 "**下一步**"。

    > [!NOTE]
    > 如果选择了本地数据库文件（而不是连接至 SQL Server），系统可能会询问你是否将该文件添加到项目中。 选择 **"是"** 将数据库文件添加到项目。

7. 在 "将**连接字符串保存到应用程序配置文件**" 页上选择 "**下一步**"。

8. 在 **“选择数据库对象”** 页面上展开 **“表”** 节点。

9. 选中 " **Customers** " 和 " **Orders** " 表的复选框，然后选择 "**完成**"。

     将 NorthwindDataSet 添加到 DataAccessTier 项目后即会显示在“数据源”窗口内。

## <a name="separate-the-tableadapters-from-the-dataset"></a>将 Tableadapter 与数据集分离
创建数据集后，接着是要将生成的数据集类与 TableAdapter 分离。 通过将“数据集项目”属性设置为要用于存储分离出的数据集类的项目的名称，可以达到此目的。

### <a name="to-separate-the-tableadapters-from-the-dataset"></a>将 TableAdapter 与数据集分离

1. 在“解决方案资源管理器”中双击“NorthwindDataSet.xsd”，以在“数据集设计器”中打开该数据集。

2. 选择设计器上的空白区域。

3. 在“属性”窗口中查找“数据集项目”节点。

4. 在 "**数据集项目**" 列表中，选择 " **DataEntityTier**"。

5. 在“生成”菜单上，选择“生成解决方案”。

   将数据集和 TableAdapter 分离到两个类库项目中。 最初包含整个数据集（`DataAccessTier`）的项目现在仅包含 Tableadapter。 **数据集项目**属性（`DataEntityTier`）中指定的项目包含类型化数据集： *NorthwindDataSet* （或*NorthwindDataSet.Dataset.Designer.cs*）。

> [!NOTE]
> 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，将不会自动移动项目中现有的数据集分部类。 你必须手动将它们移到数据集项目中。

## <a name="create-a-new-service-application"></a>创建新的服务应用程序
本演练演示如何使用 WCF 服务访问数据访问层，因此让我们创建一个新的 WCF 服务应用程序。

### <a name="to-create-a-new-wcf-service-application"></a>创建新的 WCF 服务应用程序

1. 右键单击“解决方案资源管理器”中的解决方案，然后选择“添加” > “新建项目”。

2. 在 "**新建项目**" 对话框的左侧窗格中，选择 " **WCF**"。 在中间窗格中，选择 " **WCF 服务库**"。

3. 将项目命名为**DataService** ，然后选择 **"确定"** 。

     DataService 项目即被创建并添加到 NTierWalkthrough 解决方案中。

## <a name="create-methods-in-the-data-access-tier-to-return-the-customers-and-orders-data"></a>在数据访问层中创建用于返回客户和订单数据的方法
数据服务必须在数据访问层中调用两种方法： `GetCustomers` 和 `GetOrders`。 这些方法返回 Northwind `Customers` 和 `Orders` 表。 在 `DataAccessTier` 项目中创建 `GetCustomers` 和 `GetOrders` 方法。

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-customers-table"></a>在数据访问层中创建返回 Customers 表的方法

1. 在**解决方案资源管理器**中，双击 " **NorthwindDataset** " 以打开数据集。

2. 右键单击**CustomersTableAdapter** ，然后单击 "**添加查询**"。

3. 在“选择命令类型”页面上，保留“使用 SQL 语句”的默认值，然后单击“下一步”。

4. 在“选择查询类型”页面上，保留“选择返回行”的默认值，然后单击“下一步”。

5. 在“指定 SQL SELECT 语句”页面上，保留默认查询，然后单击“下一步”。

6. 在“选择要生成的方法”页面上，为“返回 DataTable”部分的“方法名称”键入“GetCustomers”。

7. 单击 **“完成”** 。

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-orders-table"></a>在数据访问层中创建返回 Orders 表的方法

1. 右键单击“OrdersTableAdapter”，然后单击“添加查询”。

2. 在“选择命令类型”页面上，保留“使用 SQL 语句”的默认值，然后单击“下一步”。

3. 在“选择查询类型”页面上，保留“选择返回行”的默认值，然后单击“下一步”。

4. 在“指定 SQL SELECT 语句”页面上，保留默认查询，然后单击“下一步”。

5. 在“选择要生成的方法”页面上，为“返回 DataTable”部分的“方法名称”键入“GetOrders”。

6. 单击 **“完成”** 。

7. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

## <a name="add-a-reference-to-the-data-entity-and-data-access-tiers-to-the-data-service"></a>向数据服务添加对数据实体和数据访问层的引用
由于数据服务需要数据集和 TableAdapter 中的信息，因此需要添加对“DataEntityTier”和“DataAccessTier”项目的引用。

### <a name="to-add-references-to-the-data-service"></a>添加对数据服务的引用

1. 在“解决方案资源管理器”中右键单击 DataService，然后单击“添加引用”。

2. 在“添加引用”对话框中，单击“项目”选项卡。

3. 选择“DataAccessTier”和“DataEntityTier”项目。

4. 单击“确定”。

## <a name="add-functions-to-the-service-to-call-the-getcustomers-and-getorders-methods-in-the-data-access-tier"></a>向服务添加函数以调用数据访问层中的 GetCustomers 和 GetOrders 方法
现在数据访问层包含返回数据的方法，接下来要在数据服务中创建调用这些方法的方法。

> [!NOTE]
> 对于 C# 项目，必须添加对 `System.Data.DataSetExtensions` 程序集的引用，才能编译下面的代码。

### <a name="to-create-the-getcustomers-and-getorders-functions-in-the-data-service"></a>在数据服务中创建 GetCustomers 和 GetOrders 函数

1. 在“DataService”项目中，双击“IService1.vb”或“IService1.cs”。

2. 在“在此处添加服务操作”注释的下方添加以下代码：

    ```vb
    <OperationContract()> _
    Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable

    <OperationContract()> _
    Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable
    ```

    ```csharp
    [OperationContract]
    DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers();

    [OperationContract]
    DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders();
    ```

3. 在 DataService 项目中，双击“Service1.vb”（或“Service1.cs”）。

4. 将以下代码添加到“Service1”类中：

    ```vb
    Public Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable Implements IService1.GetCustomers
        Dim CustomersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
        Return CustomersTableAdapter1.GetCustomers()
    End Function

    Public Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable Implements IService1.GetOrders
        Dim OrdersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
        Return OrdersTableAdapter1.GetOrders()
    End Function
    ```

    ```csharp
    public DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
             CustomersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter();
        return CustomersTableAdapter1.GetCustomers();
    }
    public DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
             OrdersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter();
        return OrdersTableAdapter1.GetOrders();
    }
    ```

5. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

## <a name="create-a-presentation-tier-to-display-data-from-the-data-service"></a>创建表示层以显示数据服务中的数据
现在，解决方案包含的数据服务包含方法（这些方法调入数据访问层），接下来创建一个调用数据服务并向用户显示数据的项目。 对于本演练，创建一个 Windows 窗体应用程序；它将充当 N 层应用程序的表示层。

### <a name="to-create-the-presentation-tier-project"></a>创建表示层项目

1. 右键单击“解决方案资源管理器”中的解决方案，然后选择“添加” > “新建项目”。

2. 在 "**新建项目**" 对话框的左侧窗格中，选择 " **Windows 桌面**"。 在中间窗格中，选择 " **Windows 窗体应用**"。

3. 将该项目命名为“PresentationTier”，然后单击“确定”。

    PresentationTier 项目即被创建并添加到 NTierWalkthrough 解决方案中。

## <a name="set-the-presentationtier-project-as-the-startup-project"></a>将 PresentationTier 项目设置为启动项目
我们会将**PresentationTier**项目设置为解决方案的启动项目，因为它是显示数据并与之交互的实际客户端应用程序。

### <a name="to-set-the-new-presentation-tier-project-as-the-startup-project"></a>将新的表示层项目设置为启动项目

- 在“解决方案资源管理器”中，右键单击“PresentationTier”，然后单击“设为启动项目”。

## <a name="add-references-to-the-presentation-tier"></a>添加对表示层的引用
客户端应用程序 PresentationTier 需要具有对数据服务的服务引用，才能访问服务中的方法。 另外，WCF 服务又需要具有对数据集的引用，才能启用类型共享。 在通过数据服务启用类型共享之前，添加到部分数据集类的代码对表示层不可用。 由于通常会将代码（如验证代码）添加到数据表的行和列更改事件，因此可能需要从客户端访问此代码。

### <a name="to-add-a-reference-to-the-presentation-tier"></a>添加定义表示层的引用

1. 在**解决方案资源管理器**中，右键单击**PresentationTier** ，然后选择 "**添加引用**"。

2. 在 "**添加引用**" 对话框中，选择 "**项目**" 选项卡。

3. 选择**DataEntityTier**并选择 **"确定"** 。

### <a name="to-add-a-service-reference-to-the-presentation-tier"></a>添加对表示层的服务引用

1. 在**解决方案资源管理器**中，右键单击**PresentationTier** ，然后选择 "**添加服务引用**"。

2. 在 "**添加服务引用**" 对话框中，选择 "**发现**"。

3. 选择**Service1**并选择 **"确定"** 。

    > [!NOTE]
    > 如果当前计算机上有多个服务，则选择之前在本演练中创建的服务（包含 `GetCustomers` 和 `GetOrders` 方法的服务）。

## <a name="add-datagridviews-to-the-form-to-display-the-data-returned-by-the-data-service"></a>将 Datagridview 添加添加到窗体，以显示数据服务返回的数据
在添加对数据服务的服务引用后，将自动使用该服务返回的数据填充“数据源”窗口。

### <a name="to-add-two-data-bound-datagridviews-to-the-form"></a>将两个数据绑定 DataGridView 添加到窗体中

1. 在“解决方案资源管理器”中，选择“PresentationTier”项目。

2. 在“数据源”窗口中，展开“NorthwindDataSet”，然后查找“Customers”节点。

3. 将“Customers”节点拖到 Form1 上。

4. 在“数据源”窗口中，展开“Customers”节点，然后查找相关的“Orders”节点（“Orders”节点嵌套在“Customers”节点中）。

5. 将相关的“Orders”节点拖到 Form1 上。

6. 通过双击窗体的空白区域，创建一个 `Form1_Load` 事件处理程序。

7. 将以下代码添加到 `Form1_Load` 事件处理程序中。

    ```vb
    Dim DataSvc As New ServiceReference1.Service1Client
    NorthwindDataSet.Customers.Merge(DataSvc.GetCustomers)
    NorthwindDataSet.Orders.Merge(DataSvc.GetOrders)
    ```

    ```csharp
    ServiceReference1.Service1Client DataSvc =
        new ServiceReference1.Service1Client();
    northwindDataSet.Customers.Merge(DataSvc.GetCustomers());
    northwindDataSet.Orders.Merge(DataSvc.GetOrders());
    ```

## <a name="increase-the-maximum-message-size-allowed-by-the-service"></a>增加服务允许的最大消息大小
@No__t_0 的默认值不够大，无法保存从 `Customers` 和 `Orders` 表中检索的数据。 在下面的步骤中，将值增加到6553600。 您可以更改客户端上的值，这会自动更新服务引用。

> [!NOTE]
> 较小的默认大小旨在降低遭受拒绝服务 (DoS) 攻击的可能性。 有关更多信息，请参见<xref:System.ServiceModel.WSHttpBindingBase.MaxReceivedMessageSize%2A>。

### <a name="to-increase-the-maxreceivedmessagesize-value"></a>增加 maxReceivedMessageSize 值

1. 在“解决方案资源管理器”的“PresentationTier”项目中，双击“app.config”文件。

2. 查找“maxReceivedMessage”大小属性，然后将该值更改为 `6553600`。

## <a name="test-the-application"></a>测试应用程序
按 F5 运行应用程序。 从数据服务检索 `Customers` 和 `Orders` 表中的数据，并在窗体上显示这些数据。

## <a name="next-steps"></a>后续步骤
根据应用程序的需求，在基于 Windows 的应用程序中保存相关数据后，可能还要执行一些步骤。 例如，你可以对此应用程序进行以下增强：

- 将验证添加到数据集。

- 将其他方法添加到服务，以将数据更新回数据库。

## <a name="see-also"></a>请参阅

- [在 N 层应用程序中使用数据集](../data-tools/work-with-datasets-in-n-tier-applications.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)