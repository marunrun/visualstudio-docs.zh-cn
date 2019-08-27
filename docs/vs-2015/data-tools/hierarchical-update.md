---
title: 分层更新 |Microsoft Docs
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
- saving data, changed data
- data [Visual Basic], hierarchical update
- saving updated data
- datasets [Visual Basic], hierarchical update
- hierarchical update
- saving data, hierarchical update
- modified data saving
- updated data saving
- related tables, saving
ms.assetid: 68bae3f6-ec9b-45ee-a33a-69395029f54c
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 521f878c9d4fafa61f8c717f4c9752622ef339d9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699815"
---
# <a name="hierarchical-update"></a>分层更新
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分层更新 * 是指同时保持引用完整性规则保存更新后 （从具有两个或多个相关表的数据集） 返回到数据库的数据的过程。 *引用完整性*指提供的控制行为的插入、 更新和删除相关的记录在数据库中的约束的一致性规则。 例如，它是强制执行之前允许该客户的订单来创建客户记录的创建的引用完整性。  有关数据集中的关系的详细信息，请参阅[数据集中的关系](../data-tools/relationships-in-datasets.md)  
  
 分层更新功能使用`TableAdapterManager`来管理`TableAdapter`中类型化数据集。 `TableAdapterManager`组件是[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]-生成类，因此它不属于[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]。 将表从数据源窗口拖到 Windows 窗体或 WPF 页后，Visual Studio 将类型 TableAdapterManager 的变量添加到窗体或页面，和你在组件栏中的设计器中看到它。 有关详细信息`TableAdapterManager`类，请参阅的 TableAdapterManager 参考部分[TableAdapterManager 概述](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)。  
  
 默认情况下，数据集视为相关的表"，关系"这意味着它不会强制外键约束。 可以通过使用数据集设计器来修改在设计时进行该设置。 选择要显示的两个表之间的关系线**关系**对话框。 您在此处进行的更改将确定 TableAdapterManager 的行为方式时它将所做的更改在相关表中发送回数据库。  
  
## <a name="enablehierarchical-update-in-a-dataset"></a>在数据集中的 Enablehierarchical 更新  
 默认情况下，加上或在项目中创建所有新数据集启用分层更新。 通过设置打开或关闭分层更新**分层更新**属性中为数据集设计器的类型化数据集**True**或**False**:  
  
 ![分层更新设置](../data-tools/media/hierarchical-update-setting.png "分层更新设置")  
  
## <a name="create-a-new-relation-between-tables"></a>创建新表之间的关系  
 若要创建两个表之间新的关系，在数据集设计器中，选择每个表的标题栏，然后右键单击并选择**添加关系**。  
  
 ![分层更新添加关系菜单](../data-tools/media/hierarchical-update-add-relation-menu.png "分层更新添加关系菜单")  
  
## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>了解 foreign key 约束、 级联更新和删除  
 务必要了解如何 foreign key 约束和级联行为，在数据库中生成的数据集代码中创建。  
  
 默认情况下，在数据集中数据表生成关系 (<xref:System.Data.DataRelation>) 匹配的关系数据库中。 但是，在数据集中的关系不会生成作为外键约束。 <xref:System.Data.DataRelation>配置为**关系仅**而无需<xref:System.Data.ForeignKeyConstraint.UpdateRule%2A>或<xref:System.Data.ForeignKeyConstraint.DeleteRule%2A>生效。  
  
 默认情况下，级联更新和级联删除操作会关闭即使数据库关系设置级联更新和/或级联删除开启。 例如，创建新客户和新的订单，并尝试将数据保存可以导致冲突的数据库中定义 foreign key 约束。 有关详细信息，请参阅[如何：在数据集中配置外键约束](https://msdn.microsoft.com/library/3954c388-e209-4a67-a34e-5ca106282f8e)。  
  
## <a name="set-the-order-to-perform-updates"></a>设置以执行更新的顺序  
 设置的顺序来执行更新集个人的顺序插入、 更新和删除，需要将所有修改后的数据保存在数据集的所有表。 启用分层更新后，插入第一次，执行，然后更新，，然后删除。 `TableAdapterManager`提供了`UpdateOrder`可以是组以执行更新第一次，然后插入和删除操作的属性。  
  
> [!NOTE]
> 请务必了解，更新顺序是全包含所有权限。 也就是说时不会进行更新，, 插入和删除执行在数据集中的所有表。  
  
 若要设置`UpdateOrder`属性，则请将某些项从[数据源窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)拖到窗体中，选择`TableAdapterManager`在组件栏，然后将设置`UpdateOrder`中的属性**属性**窗口。 有关详细信息，请参阅[如何：执行分层更新时设置的顺序](https://msdn.microsoft.com/library/a0734935-78dd-4c0b-80d7-5e7925789c83)。  
  
## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>执行分层更新前创建一个数据集的备份副本  
 在您保存数据 (通过调用`TableAdapterManager.UpdateAll()`方法)，则`TableAdapterManager`尝试更新每个表在单个事务中的数据。 如果任何表的更新的任何部分失败，将回滚整个事务。 在大多数情况下，回滚返回到其原始状态的应用程序。  
  
 但是，有时你可能想要从备份副本还原数据集。 使用自动递增的值时，可能会出现的一个例子。 例如，如果保存操作不成功、 自动递增的值不会重置数据集和数据集将继续创建自动递增的值。这将使编号中间隙，可能不在你的应用程序中可接受的。 在的情况下这是一个问题，其中`TableAdapterManager`提供了`BackupDataSetBeforeUpdate`用备份副本替换现有数据集，如果事务失败时的属性。  
  
> [!NOTE]
> 备份副本是在内存中时`TableAdapterManager.UpdateAll`方法是否正在运行。 因此，没有此备份的数据集不能以编程方式访问因为它将替换原始数据集或超出范围后`TableAdapterManager.UpdateAll`方法完成运行。  
  
## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>修改生成保存代码以执行分层更新  
 通过调用 `TableAdapterManager.UpdateAll` 方法并传入包含相关表的数据集的名称，可将数据集中相关数据表的更改保存到数据库。 例如，运行 `TableAdapterManager.UpdateAll(NorthwindDataset)` 方法将 NorthwindDataset 中所有表的更新发送到后端数据库。  
  
 从“数据源”窗口放置项后，代码会自动添加到 `Form_Load` 事件以填充每个表（`TableAdapter.Fill` 方法）。 代码还将添加到 <xref:System.Windows.Forms.BindingNavigator> 的“保存”按钮 click 事件中，以将数据集中的数据存回数据库中（`TableAdapterManager.UpdateAll` 方法）。  
  
 生成的保存代码还包含调用 `CustomersBindingSource.EndEdit` 方法的一行代码。 更具体地说，它将调用<xref:System.Windows.Forms.BindingSource.EndEdit%2A>方法的第一个<xref:System.Windows.Forms.BindingSource>，添加到窗体。 换而言之，此代码只为生成第一个表中拖动**数据源**拖到窗体的窗口。 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用将提交当前正在编辑的任何数据绑定控件中的所有更改。 因此，如果数据绑定控件仍具有焦点，则单击“保存”按钮后，会先提交该控件中所有挂起的编辑，然后再执行真正的保存（`TableAdapterManager.UpdateAll` 方法）。  
  
> [!NOTE]
> 数据集设计器仅添加`BindingSource.EndEdit`放到窗体的第一个表的代码。 因此，必须对窗体上的每个相关表添加一行调用 `BindingSource.EndEdit` 方法的代码。 对于本演练，这意味着你必须添加一个对 `OrdersBindingSource.EndEdit` 方法的调用。  
  
#### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>更新代码以在保存前提交对相关表的更改  
  
1. 双击 <xref:System.Windows.Forms.BindingNavigator> 上的“保存”按钮以在代码编辑器中打开“Form1”。  
  
2. 在调用 `OrdersBindingSource.EndEdit` 方法的代码行后添加一行调用 `CustomersBindingSource.EndEdit` 方法的代码。 “保存”按钮 click 事件中的代码应如下所示：  
  
    [!code-csharp[VSProDataOrcasHierarchicalUpdate#1](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs#1)]
    [!code-vb[VSProDataOrcasHierarchicalUpdate#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb#1)]  
  
   除了在将数据保存到数据库之前提交对相关子表的更改外，你可能还需要在向数据集添加新子记录之前先提交新创建的父记录。 也就是说，你可能需要先向数据集添加新父记录 (Customer)，然后外键约束才允许将新子记录 (Orders) 添加到数据集中。 为实现这一点，可以使用子 `BindingSource.AddingNew` 事件。  
  
> [!NOTE]
> 是否必须提交新的父记录取决于用于绑定到数据源的控件的类型。 在本演练中，使用单独的控件绑定到父表。 这需要额外的代码来提交新的父记录。 如果父记录中的复杂绑定控件改为显示类似于<xref:System.Windows.Forms.DataGridView>、 额外<xref:System.Windows.Forms.BindingSource.EndEdit%2A>调用父记录不是必需的。 这是因为这类控件的基础数据绑定功能可以提交新记录。  
  
#### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>添加代码以在添加新子记录之前在数据集中提交父记录  
  
1. 为 `OrdersBindingSource.AddingNew` 事件创建一个事件处理程序。  
  
    - 打开**Form1**在设计视图中，选择**OrdersBindingSource**在组件栏中，选择**事件**中**属性**窗口中，并然后双击**AddingNew**事件。  
  
2. 将一行代码添加到的事件处理程序调用`CustomersBindingSource.EndEdit`方法。 `OrdersBindingSource_AddingNew` 事件处理程序中的代码应如下所示：  
  
     [!code-csharp[VSProDataOrcasHierarchicalUpdate#2](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs#2)]
     [!code-vb[VSProDataOrcasHierarchicalUpdate#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb#2)]  
  
## <a name="tableadaptermanager-reference"></a>TableAdapterManager 引用  
 默认情况下，`TableAdapterManager`创建包含相关的表的数据集时生成类。 若要防止此类生成的值更改`Hierarchical Update`为 false 将数据集属性。 当拖放到设计图面上的 Windows 窗体或 WPF 页的关系的表时，Visual Studio 声明类的成员变量。 如果不使用数据绑定，您必须手动将该变量的声明。  
  
 `TableAdapterManager`类不是属于[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]。 因此，你不能查找其文档中。 在设计时数据集创建过程的一部分创建。  
  
 以下是常用的方法和属性`TableAdapterManager`类：  
  
|成员|描述|  
|------------|-----------------|  
|`UpdateAll` 方法|将保存数据的所有表中的所有数据。|  
|`BackUpDataSetBeforeUpdate` 属性|确定是否在执行前创建数据集的备份副本`TableAdapterManager.UpdateAll`方法。一个布尔值。|  
|*tableName* `TableAdapter`属性|表示`TableAdapter`。 生成`TableAdapterManager`包含每个属性`TableAdapter`它所管理。 例如，Customers 和 Orders 表具有的数据集生成具有`TableAdapterManager`，其中包含`CustomersTableAdapter`和`OrdersTableAdapter`属性。|  
|`UpdateOrder` 属性|控制各个 insert、 update 和 delete 命令的顺序。 将此项设置中的值之一`TableAdapterManager.UpdateOrderOption`枚举。<br /><br /> 默认情况下`UpdateOrder`设置为**InsertUpdateDelete**。 这意味着，它将插入，然后更新，然后删除会对在数据集中的所有表执行。 有关详细信息，请参阅[如何：执行分层更新时设置的顺序](https://msdn.microsoft.com/library/a0734935-78dd-4c0b-80d7-5e7925789c83)。|  
  
## <a name="see-also"></a>请参阅  
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
