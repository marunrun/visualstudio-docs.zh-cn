---
title: 查询数据集
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
ms.assetid: 7b1a91cf-8b5a-4fc0-ac36-0dc2d336fa1b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4ef1c806914b0f134702e010b58229ee3fc15c7a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281859"
---
# <a name="query-datasets"></a>查询数据集
若要搜索数据集中的特定记录，请使用 `FindBy` DataTable 上的方法，编写自己的 foreach 语句来循环遍历表的 Rows 集合，或使用[LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)。

## <a name="dataset-case-sensitivity"></a>数据集区分大小写
在数据集内，表名和列名在默认情况下是不区分大小写的，也就是说，数据集中名为 "Customers" 的表也可以称为 "customers"。 这与多个数据库中的命名约定相匹配，其中包括 SQL Server。 在 SQL Server 中，默认行为是数据元素的名称不能仅通过大小写区分。

> [!NOTE]
> 不同于数据集，XML 文档区分大小写，因此在架构中定义的数据元素的名称区分大小写。 例如，架构协议允许架构定义名为 "Customers" 的表和名为 "customers" 的其他表。 当包含仅大小写不同的元素的架构用于生成数据集类时，这可能会导致名称冲突。

然而，区分大小写是在数据集内解释数据的方式的一个因素。 例如，如果筛选数据集表中的数据，搜索条件可能会返回不同的结果，具体取决于比较是否区分大小写。 可以通过设置数据集的属性来控制筛选、搜索和排序的区分大小写 <xref:System.Data.DataSet.CaseSensitive%2A> 。 默认情况下，数据集中的所有表都继承此属性的值。 （您可以通过设置表的属性，为每个单独的表覆盖此属性 <xref:System.Data.DataTable.CaseSensitive%2A> 。）

## <a name="locate-a-specific-row-in-a-data-table"></a>查找数据表中的特定行

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>在包含主键值的类型化数据集中查找行

- 若要查找行，请调用 `FindBy` 使用该表的主键的强类型化方法。

     在下面的示例中， `CustomerID` 列是表的主键 `Customers` 。 这意味着生成的 `FindBy` 方法为 `FindByCustomerID` 。 该示例演示如何使用生成的方法将特定的分配 <xref:System.Data.DataRow> 到变量 `FindBy` 。

     [!code-csharp[VbRaddataEditing#18](../data-tools/codesnippet/CSharp/query-datasets_1.cs)]
     [!code-vb[VbRaddataEditing#18](../data-tools/codesnippet/VisualBasic/query-datasets_1.vb)]

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>在包含主键值的非类型化数据集中查找行

- 调用 <xref:System.Data.DataRowCollection.Find%2A> 集合的方法 <xref:System.Data.DataRowCollection> ，将主键作为参数传递。

     下面的示例演示如何声明一个名为的新行 `foundRow` ，并为其分配方法的返回值 <xref:System.Data.DataRowCollection.Find%2A> 。 如果找到主键，则列索引1的内容将显示在消息框中。

     [!code-csharp[VbRaddataEditing#19](../data-tools/codesnippet/CSharp/query-datasets_2.cs)]
     [!code-vb[VbRaddataEditing#19](../data-tools/codesnippet/VisualBasic/query-datasets_2.vb)]

## <a name="find-rows-by-column-values"></a>按列值查找行

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>根据任意列中的值查找行

- 数据表是使用方法创建的 <xref:System.Data.DataTable.Select%2A> ，该方法 <xref:System.Data.DataRow> 根据传递给方法的表达式返回的数组 <xref:System.Data.DataTable.Select%2A> 。 有关创建有效表达式的详细信息，请参阅有关属性页的 "表达式语法" 部分 <xref:System.Data.DataColumn.Expression%2A> 。

     下面的示例演示如何使用的 <xref:System.Data.DataTable.Select%2A> 方法 <xref:System.Data.DataTable> 来查找特定的行。

     [!code-csharp[VbRaddataEditing#20](../data-tools/codesnippet/CSharp/query-datasets_3.cs)]
     [!code-vb[VbRaddataEditing#20](../data-tools/codesnippet/VisualBasic/query-datasets_3.vb)]

## <a name="access-related-records"></a>访问相关记录
如果数据集中的表相关，则 <xref:System.Data.DataRelation> 对象可以使相关记录在其他表中可用。 例如， `Customers` 可以提供包含和表的数据集 `Orders` 。

<xref:System.Data.DataRelation>通过 <xref:System.Data.DataRow.GetChildRows%2A> <xref:System.Data.DataRow> 在父表中调用的方法，可以使用对象来查找相关记录。 此方法返回相关子记录的数组。 或者，你可以 <xref:System.Data.DataRow.GetParentRow%2A> <xref:System.Data.DataRow> 在子表中调用的方法。 此方法 <xref:System.Data.DataRow> 从父表返回单个。

本页提供使用类型化数据集的示例。 有关在非类型化数据集中导航关系的信息，请参阅[导航 datarelation](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations)。

> [!NOTE]
> 如果使用的是 Windows 窗体应用程序并使用数据绑定功能显示数据，则设计器生成的窗体可能会为应用程序提供足够的功能。 有关详细信息，请参阅[在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。 具体而言，请参阅[数据集中的关系](relationships-in-datasets.md)。

下面的代码示例演示如何在类型化的数据集中向上和向下导航关系。 此代码示例使用类型化 <xref:System.Data.DataRow> `NorthwindDataSet.OrdersRow` 的（）和生成的 FindBy*PrimaryKey* （ `FindByCustomerID` ）方法查找所需的行并返回相关记录。 仅当有以下情况时，才会正确编译和运行示例：

- 使用表命名的数据集的实例 `NorthwindDataSet` `Customers` 。

- 一个 `Orders` 表。

- 名称 `FK_Orders_Customers` 与两个表相关的关系。

另外，这两个表都需要为要返回的任何记录填充数据。

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>返回选定父记录的子记录

- 调用 <xref:System.Data.DataRow.GetChildRows%2A> 特定数据行的方法 `Customers` ，并从表中返回行的数组 `Orders` ：

     [!code-csharp[VbRaddataDatasets#6](../data-tools/codesnippet/CSharp/query-datasets_4.cs)]
     [!code-vb[VbRaddataDatasets#6](../data-tools/codesnippet/VisualBasic/query-datasets_4.vb)]

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>返回选定子记录的父记录

- 调用 <xref:System.Data.DataRow.GetParentRow%2A> 特定数据行的方法 `Orders` ，并从表中返回一行 `Customers` ：

     [!code-csharp[VbRaddataDatasets#7](../data-tools/codesnippet/CSharp/query-datasets_5.cs)]
     [!code-vb[VbRaddataDatasets#7](../data-tools/codesnippet/VisualBasic/query-datasets_5.vb)]

## <a name="see-also"></a>请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
