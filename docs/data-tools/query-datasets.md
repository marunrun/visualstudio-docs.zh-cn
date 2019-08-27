---
title: 查询数据集
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 7b1a91cf-8b5a-4fc0-ac36-0dc2d336fa1b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: bec1c878dce59ccb5444d74ba0255c9ceb705780
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402744"
---
# <a name="query-datasets"></a>查询数据集
若要搜索在数据集中的特定记录，请使用`FindBy`方法在 DataTable，编写自己的 foreach 语句循环访问表的行集合，或使用[LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)。

## <a name="dataset-case-sensitivity"></a>数据集的区分大小写
在一个数据集、 表和列的名称是默认情况下不区分大小写，即，表中一个称为"客户"数据集可以也称为"customers。 此匹配在多个数据库，包括 SQL Server 中的命名约定。 在 SQL Server 中，默认行为是，不能只是大小写区分的数据元素的名称。

> [!NOTE]
> 与不同的数据集、 XML 文档不区分大小写，因此在架构中定义的数据元素的名称是区分大小写。 例如，架构协议允许定义名为"客户"和一个名为"客户。"的不同表的表的架构 当包含仅大小写不同的元素的架构用于生成数据集类时，这可能导致名称冲突。

区分大小写，但是，可以是数据集内如何解释数据的一个因素。 例如，如果数据集表中的数据进行筛选，搜索条件可能返回不同的结果，具体取决于比较是否区分大小写。 您可以控制是否区分大小写的筛选、 搜索和排序通过设置数据集的<xref:System.Data.DataSet.CaseSensitive%2A>属性。 默认情况下，在数据集中的所有表都继承此属性的值。 (可以通过设置表的重写此属性对于每个表<xref:System.Data.DataTable.CaseSensitive%2A>属性。)

## <a name="locate-a-specific-row-in-a-data-table"></a>在数据表中查找特定行

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>若要在具有主键值的类型化数据集查找的行

- 若要查找行，调用强类型化`FindBy`方法，它使用表的主键。

     在以下示例中，`CustomerID`列是主键的`Customers`表。 这意味着，生成`FindBy`方法是`FindByCustomerID`。 该示例演示如何将分配一个特定<xref:System.Data.DataRow>通过使用生成变量`FindBy`方法。

     [!code-csharp[VbRaddataEditing#18](../data-tools/codesnippet/CSharp/query-datasets_1.cs)]
     [!code-vb[VbRaddataEditing#18](../data-tools/codesnippet/VisualBasic/query-datasets_1.vb)]

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>若要在具有主键值的非类型化数据集查找的行

- 调用<xref:System.Data.DataRowCollection.Find%2A>方法的<xref:System.Data.DataRowCollection>集合，作为参数传递的主键。

     下面的示例演示如何声明一个名为的新行`foundRow`并将其分配的返回值<xref:System.Data.DataRowCollection.Find%2A>方法。 如果找到的主键，则在消息框中显示的列索引 1 内容。

     [!code-csharp[VbRaddataEditing#19](../data-tools/codesnippet/CSharp/query-datasets_2.cs)]
     [!code-vb[VbRaddataEditing#19](../data-tools/codesnippet/VisualBasic/query-datasets_2.vb)]

## <a name="find-rows-by-column-values"></a>查找行的列的值

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>若要查找任何列中的值的行

- 使用创建数据表<xref:System.Data.DataTable.Select%2A>方法，返回的数组<xref:System.Data.DataRow>s 基于表达式传递给<xref:System.Data.DataTable.Select%2A>方法。 有关创建有效的表达式的详细信息，请参阅页的"表达式语法"部分<xref:System.Data.DataColumn.Expression%2A>属性。

     下面的示例演示如何使用<xref:System.Data.DataTable.Select%2A>方法的<xref:System.Data.DataTable>来查找特定行。

     [!code-csharp[VbRaddataEditing#20](../data-tools/codesnippet/CSharp/query-datasets_3.cs)]
     [!code-vb[VbRaddataEditing#20](../data-tools/codesnippet/VisualBasic/query-datasets_3.vb)]

## <a name="access-related-records"></a>访问相关的记录
当在数据集中的表进行关联时，<xref:System.Data.DataRelation>对象可以使相关的记录在另一个表中可用。 例如，一个数据集，其中包含`Customers`和`Orders`表便可提供。

可以使用<xref:System.Data.DataRelation>要通过调用来查找相关的记录对象<xref:System.Data.DataRow.GetChildRows%2A>方法的<xref:System.Data.DataRow>父表中。 此方法返回的相关的子记录的数组。 或者，可以致电<xref:System.Data.DataRow.GetParentRow%2A>方法的<xref:System.Data.DataRow>子表中。 此方法返回单个<xref:System.Data.DataRow>从父表。

此页提供了示例使用类型化数据集。 有关在非类型化数据集中的关系中导航的信息，请参阅[导航 Datarelation](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations)。

> [!NOTE]
> 如果您正在使用 Windows 窗体应用程序和使用数据绑定功能显示数据，设计器生成的表单可能会提供足够的功能为应用程序。 有关详细信息，请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。 具体而言，请参阅[中的数据集的关系](relationships-in-datasets.md)。

下面的代码示例演示如何导航向上和向下中类型化数据集的关系。 代码示例使用类型化<xref:System.Data.DataRow>s (`NorthwindDataSet.OrdersRow`) 和生成的 FindBy*PrimaryKey* (`FindByCustomerID`) 方法来查找所需的行并返回相关的记录。 示例编译并正常运行，仅在必须：

- 名为的数据集的实例`NorthwindDataSet`与`Customers`表。

- `Orders`表。

- 关系名为`FK_Orders_Customers`相关的两个表。

此外，这两个表需要填充要返回的任何记录的数据。

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>若要返回的子记录所选的父记录

- 调用<xref:System.Data.DataRow.GetChildRows%2A>方法的特定`Customers`数据行，并返回一个数组中的行`Orders`表：

     [!code-csharp[VbRaddataDatasets#6](../data-tools/codesnippet/CSharp/query-datasets_4.cs)]
     [!code-vb[VbRaddataDatasets#6](../data-tools/codesnippet/VisualBasic/query-datasets_4.vb)]

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>若要返回的所选的子记录的父记录

- 调用<xref:System.Data.DataRow.GetParentRow%2A>方法的特定`Orders`数据行，并返回单个行从`Customers`表：

     [!code-csharp[VbRaddataDatasets#7](../data-tools/codesnippet/CSharp/query-datasets_5.cs)]
     [!code-vb[VbRaddataDatasets#7](../data-tools/codesnippet/VisualBasic/query-datasets_5.vb)]

## <a name="see-also"></a>请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)