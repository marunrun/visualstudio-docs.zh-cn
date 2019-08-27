---
title: 演练：自定义插入、 更新和删除实体类的行为 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 03ff1146-706e-4780-91cb-56a83df63eea
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: db27e8665d74477f3bb668831cbfaeef00d622bd
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700218"
---
# <a name="walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes"></a>演练：自定义实体类的插入、更新和删除行为
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[LINQ to SQL 工具在 Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)提供一个可视化设计图面，用于创建和编辑[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)]基于数据库中的对象的类 （实体类）。 通过使用[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)，可以使用 LINQ 技术访问 SQL 数据库。 有关详细信息，请参阅 [LINQ（语言集成查询）](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)。  
  
 默认情况下，由 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 运行时提供用于执行更新的逻辑。 该运行时基于表的架构（列定义和主键信息）创建默认的 Insert、Update 和 Delete 语句。 当不希望使用默认行为时，可以配置更新行为并指定特定的存储过程，来执行处理数据库中数据所必需的插入、更新和删除。 在不生成默认行为时（例如，实体类映射到视图时），也可以这样做。 另外，在数据库要求通过存储过程访问表时，您可以重写默认的更新行为。 有关详细信息，请参阅[自定义操作通过使用存储过程](https://msdn.microsoft.com/library/aedbecc1-c33c-4fb4-8861-fdf7e1dc6b8a)。  
  
> [!NOTE]
> 本演练要求可以使用 Northwind 数据库的“InsertCustomer”、“UpdateCustomer”和“DeleteCustomer”存储过程。
  
 本演练提供了一些步骤，您必须执行这些步骤来重写默认的 LINQ to SQL 运行时行为，以便使用存储过程将数据保存回数据库。  
  
 在本演练中，你将学习如何执行以下任务：  
  
- 创建一个新的 Windows 窗体应用程序，并将一个 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 文件添加到该应用程序。  
  
- 创建一个映射到 Northwind Customers 表的实体类。  
  
- 创建一个引用 LINQ to SQL Customer 类的对象数据源。  
  
- 创建一个包含绑定到 Customer 类的 <xref:System.Windows.Forms.DataGridView> 的 Windows 窗体。  
  
- 实现该窗体的保存功能。  
  
- 通过将存储过程添加到 <xref:System.Data.Linq.DataContext>来创建 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 方法。  
  
- 配置 Customer 类以使用存储过程执行插入、更新和删除。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成此演练，需要满足以下条件：  
  
- 访问 Northwind 示例数据库的 SQL Server 版本。
  
- **InsertCustomer**， **UpdateCustomer**，并**DeleteCustomer**存储 Northwind 数据库的过程。
  
## <a name="creating-an-application-and-adding-linq-to-sql-classes"></a>创建一个应用程序并添加 LINQ to SQL 类  
 因为您将要使用 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 类并在 Windows 窗体中显示数据，所以需要创建一个新的 Windows 窗体应用程序并添加一个 LINQ to SQL 类文件。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-create-a-new-windows-application-project-that-contains-linq-to-sql-classes"></a>新建一个包含 LINQ to SQL 类的 Windows 应用程序项目  
  
1. 从**文件**菜单中，创建一个新项目。  
  
2. 将项目命名**UpdatingwithSProcsWalkthrough**。  
  
    > [!NOTE]
    > [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 和 C# 项目都支持 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]。 因此，请使用这两种语言之一创建新项目。  
  
3. 单击**Windows 窗体应用程序**模板，然后单击**确定**。 有关详细信息，请参阅[客户端应用程序](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)。  
  
     创建 UpdatingwithSProcsWalkthrough 项目并将其添加到**解决方案资源管理器**。  
  
4. 在 **“项目”** 菜单上，单击 **“添加新项”**。  
  
5. 单击“LINQ to SQL 类”模板，然后在“名称”框中键入 Northwind.dbml。  
  
6. 单击 **添加**。  
  
     这会将一个空的 LINQ to SQL 类文件 (Northwind.dbml) 添加到该项目中，并且会打开 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。  
  
## <a name="creating-the-customer-entity-class-and-object-data-source"></a>创建 Customer 实体类和对象数据源  
 创建[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)]通过将从映射到数据库表的类**服务器资源管理器**/**数据库资源管理器**拖到[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。 结果将生成映射到数据库中的表的 LINQ to SQL 实体类。 在创建实体类后，可以将这些类像具有公共属性的其他类一样用作对象数据源。  
  
#### <a name="to-create-a-customer-entity-class-and-configure-a-data-source-with-it"></a>创建 Customer 实体类并使用该类配置数据源  
  
1. 在中**服务器资源管理器**/**数据库资源管理器**，查找 Northwind 示例数据库的 SQL Server 版本中的客户表。
  
2. 拖动**客户**从节点**服务器资源管理器**/**数据库资源管理器**到[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]图面。  
  
     将创建一个名为“Customer”的实体类。 该类具有与 Customers 表中的列相对应的属性。 由于该实体类表示 Customers 表中的单个客户，因此将该类命名为“Customer”（而不是“Customers”）。  
  
    > [!NOTE]
    > 这种重命名行为称为“复数化”。 可以通过启用或禁用[选项对话框](../ide/reference/options-dialog-box-visual-studio.md)。 有关详细信息，请参阅[如何：打开和关闭复数形式（O/R 设计器）](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md)。  
  
3. 在“生成”菜单上单击“生成 UpdatingwithSProcsWalkthrough”以生成该项目。  
  
4. 在 **“数据”** 菜单上，单击 **“显示数据源”**。  
  
5. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。  
  
6. 单击“选择数据源类型”页上的“对象”，然后单击“下一步”。  
  
7. 展开“UpdatingwithSProcsWalkthrough”节点，然后找到并选择“Customer”类。  
  
    > [!NOTE]
    > 如果“Customer”类不可用，则退出向导，生成项目，然后重新运行向导。  
  
8. 单击“完成”以创建数据源，并将“Customer”实体类添加到“数据源”窗口。  
  
## <a name="creating-a-datagridview-to-display-the-customer-data-on-a-windows-form"></a>创建一个 DataGridView 以在 Windows 窗体中显示 Customer 数据  
 创建控件绑定到实体类通过拖动[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)]数据源项从**数据源**拖到 Windows 窗体的窗口。  
  
#### <a name="to-add-controls-that-are-bound-to-the-entity-classes"></a>添加绑定到实体类的控件  
  
1. 在“设计”视图中打开“Form1”。  
  
2. 从**数据源**窗口中，拖动**客户**节点拖到 Form1 上的。  
  
    > [!NOTE]
    > 若要显示“数据源”窗口，请单击“数据”菜单上的“显示数据源”。  
  
3. 在代码编辑器中打开 Form1。  
  
4. 将下面的代码添加到该窗体中。这些代码对于该窗体是全局性的，位于任何特定方法之外，但位于 Form1 类内部：  
  
    ```vb  
    Private NorthwindDataContext1 As New NorthwindDataContext  
    ```  
  
    ```csharp  
    private NorthwindDataContext northwindDataContext1  
        = new NorthwindDataContext();  
  
    ```  
  
5. 为 `Form_Load` 事件创建一个事件处理程序，并将下面的代码添加到该处理程序中：  
  
    ```vb  
    CustomerBindingSource.DataSource = NorthwindDataContext1.Customers  
    ```  
  
    ```csharp  
    customerBindingSource.DataSource  
        = northwindDataContext1.Customers;  
  
    ```  
  
## <a name="implementing-save-functionality"></a>实现保存功能  
 默认情况下，没有启用保存按钮，也没有实现保存功能。 此外，在为对象数据源创建数据绑定控件时，不会自动添加用于将更改后的数据保存到数据库的代码。 本节说明如何为 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 对象启用保存按钮并实现保存功能。  
  
#### <a name="to-implement-save-functionality"></a>实现保存功能  
  
1. 在“设计”视图中打开“Form1”。  
  
2. 在“CustomerBindingNavigator”上选择保存按钮（带有软盘图标的按钮）。  
  
3. 在“属性”窗口中，将“Enabled”属性设置为“True”。  
  
4. 双击保存按钮以创建一个事件处理程序并切换到代码编辑器。  
  
5. 将下面的代码添加到保存按钮事件处理程序中：  
  
    ```vb  
    NorthwindDataContext1.SubmitChanges()  
    ```  
  
    ```csharp  
    northwindDataContext1.SubmitChanges();  
    ```  
  
## <a name="overriding-the-default-behavior-for-performing-updates-inserts-updates-and-deletes"></a>重写用于执行更新（插入、更新和删除）的默认行为  
  
#### <a name="to-override-the-default-update-behavior"></a>重写默认更新行为  
  
1. 在 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中打开“LINQ to SQL”文件。 （在“解决方案资源管理器”中双击“Northwind.dbml”文件。）  
  
2. 在中**服务器资源管理器**/**数据库资源管理器**，展开 Northwind 数据库**存储过程**节点并找到**InsertCustomers**， **UpdateCustomers**，和**DeleteCustomers**存储过程。  
  
3. 将所有这三个存储过程都拖动到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]上。  
  
     这些存储过程将作为 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格中。 有关详细信息，请参阅[DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。  
  
4. 选择**客户**中的实体类[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。  
  
5. 在“属性”窗口中选择“Insert”属性。  
  
6. 单击省略号 （...） 下一步**使用运行时**以打开**配置行为**对话框。  
  
7. 选择“自定义”。  
  
8. 在“自定义”列表中选择“InsertCustomers”方法。  
  
9. 单击“应用”保存所选择的类和行为的配置。  
  
    > [!NOTE]
    > 只要在每次更改后单击“应用”，就可以继续为每个类/行为组合配置行为。 如果您更改的类或行为之前单击**应用**、 提供商机应用任何更改将出现一个警告对话框。  
  
10. 在“行为”列表中选择“更新”。  
  
11. 选择“自定义”。  
  
12. 在“自定义”列表中选择“UpdateCustomers”方法。  
  
     检查“方法参数”和“类属性”列表，会注意到，对于表中的某些列，有两个“方法参数”和两个“类属性”。 这样可以更加轻松地跟踪更改和创建检查并发冲突的语句。  
  
13. 将“Original_CustomerID”方法参数映射到“CustomerID (Original)”类属性。  
  
    > [!NOTE]
    > 默认情况下，当名称匹配时，方法自变量会映射到类属性。 如果属性名称发生更改并且在表与实体类之间不再匹配，则在 O/R 设计器无法确定正确的映射时，您可能必须选择等效的类属性进行映射。 此外，如果方法参数没有用于进行映射的有效类属性，则可以将“类属性”值设置为“(无)”。  
  
14. 单击“应用”保存所选择的类和行为的配置。  
  
15. 选择“行为”列表中的“删除”。  
  
16. 选择“自定义”。  
  
17. 在“自定义”列表中选择“DeleteCustomers”方法。  
  
18. 将“Original_CustomerID”方法参数映射到“CustomerID (Original)”类属性。  
  
19. 单击 **“确定”**。  
  
> [!NOTE]
> 在本演练中，虽然以下事实并不会产生问题，但仍然需要注意：[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 会在插入和更新操作期间自动为标识（自动递增）列、rowguidcol（数据库生成的 GUID）列以及时间戳列处理数据库生成的值。 在其他列类型中，数据库生成的值将意外导致 Null 值。 若要返回数据库生成的值，应手动将 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> 设置为 `true` 并将 <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> 设置为下列值之一：<xref:System.Data.Linq.Mapping.AutoSync>、<xref:System.Data.Linq.Mapping.AutoSync> 或 <xref:System.Data.Linq.Mapping.AutoSync>。  
  
## <a name="testing-the-application"></a>测试应用程序  
 再次运行应用程序以验证“UpdateCustomers”存储过程是否能够正确更新数据库中的客户记录。  
  
#### <a name="to-test-the-application"></a>测试应用程序  
  
1. 按 F5。  
  
2. 修改网格中的一条记录以测试更新行为。  
  
3. 添加一条新记录以测试插入行为。  
  
4. 单击“保存”按钮将更改保存回数据库。  
  
5. 关闭窗体。  
  
6. 按 F5 并验证是否保存了更新的记录和新插入的记录。  
  
7. 删除在步骤 3 中创建的新记录以测试删除行为。  
  
8. 单击保存按钮以提交更改并从数据库中移除已删除的记录  
  
9. 关闭窗体。  
  
10. 按 F5 并验证是否从数据库中移除了已删除的记录。  
  
    > [!NOTE]
    > 如果你的应用程序将使用 SQL Server Express Edition，具体取决于值**复制到输出目录**数据库文件的属性，所做的更改可能不会显示在步骤 10 中按 F5 时。
  
## <a name="next-steps"></a>后续步骤  
 根据应用程序需求的不同，您可能需要在创建 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 实体类后执行几个步骤。 你可以对此应用程序进行的一些增强包括：  
  
- 在更新过程中实现并发检查。 有关信息，请参阅[开放式并发：概述](https://msdn.microsoft.com/library/c2e38512-d0c8-4807-b30a-cb7e30338694)。  
  
- 添加 LINQ 查询以筛选数据。 有关信息，请参阅[LINQ 查询 (C#) 简介](https://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8)。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [LINQ to SQL 查询](https://msdn.microsoft.com/library/f4897aaa-7f44-4c20-a471-b948c2971aae)   
 [DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)   
 [如何：分配存储的过程以便执行更新、 插入和删除操作 （O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)   
 [PAVE What's New for Visual Studio 2012 中的数据应用程序开发](https://msdn.microsoft.com/3d50d68f-5f44-4915-842f-6d42fce793f1)
