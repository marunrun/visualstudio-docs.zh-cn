---
title: 编辑数据集中的数据
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b51b5b4be12f76e2237ff93659617e1c1843722a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586648"
---
# <a name="edit-data-in-datasets"></a>编辑数据集中的数据
编辑数据表中的数据与编辑任何数据库的表中的数据非常类似。 此过程可能包括插入、更新和删除表中的记录。 在数据绑定窗体中，可以指定哪些字段是用户可编辑的字段。 在这些情况下，数据绑定基础结构将处理所有更改跟踪，以便以后可以将更改发送回数据库。 如果以编程方式对数据进行编辑，并且想要将这些更改发送回数据库，则必须使用执行更改跟踪的对象和方法。

除了更改实际数据之外，您还可以查询 <xref:System.Data.DataTable> 以返回特定的数据行。 例如，您可以查询单独的行、行的特定版本（原始和建议）、已更改的行或有错误的行。

## <a name="to-edit-rows-in-a-dataset"></a>编辑数据集中的行
若要编辑 <xref:System.Data.DataTable>中的现有行，需要查找要编辑的 <xref:System.Data.DataRow>，然后将更新后的值分配给所需的列。

如果您不知道要编辑的行的索引，请使用 `FindBy` 方法按主键进行搜索：

[!code-csharp[VbRaddataEditing#3](../data-tools/codesnippet/CSharp/edit-data-in-datasets_1.cs)]
[!code-vb[VbRaddataEditing#3](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_1.vb)]

如果知道行索引，则可以访问和编辑行，如下所示：

[!code-csharp[VbRaddataEditing#5](../data-tools/codesnippet/CSharp/edit-data-in-datasets_2.cs)]
[!code-vb[VbRaddataEditing#5](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_2.vb)]

## <a name="to-insert-new-rows-into-a-dataset"></a>向数据集插入新行
使用数据绑定控件的应用程序通常通过[BindingNavigator 控件](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)上的 "**添加新**项" 按钮来添加新记录。

若要将新记录手动添加到数据集，请通过对 DataTable 调用方法来创建新的数据行。 然后，将该行添加到 <xref:System.Data.DataTable>的 <xref:System.Data.DataRow> 集合（<xref:System.Data.DataTable.Rows%2A>）：

[!code-csharp[VbRaddataEditing#1](../data-tools/codesnippet/CSharp/edit-data-in-datasets_3.cs)]
[!code-vb[VbRaddataEditing#1](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_3.vb)]

为了保留数据集将更新发送到数据源所需的信息，请使用 <xref:System.Data.DataRow.Delete%2A> 方法删除数据表中的行。 例如，如果应用程序使用 TableAdapter （或 <xref:System.Data.Common.DataAdapter>），则 TableAdapter 的 `Update` 方法会删除数据库中具有 <xref:System.Data.DataRow.RowState%2A> <xref:System.Data.DataRowState.Deleted>的行。

如果您的应用程序不需要将更新发送回数据源，则可以通过直接访问数据行集合（<xref:System.Data.DataRowCollection.Remove%2A>）来删除记录。

#### <a name="to-delete-records-from-a-data-table"></a>删除数据表中的记录

- 调用 <xref:System.Data.DataRow>的 <xref:System.Data.DataRow.Delete%2A> 方法。

     此方法不会以物理方式删除记录。 相反，它会将记录标记为要删除。

    > [!NOTE]
    > 如果获取 <xref:System.Data.DataRowCollection>的计数属性，则生成的计数将包含已标记为要删除的记录。 若要获取未标记为要删除的记录的准确计数，可以循环遍历集合，查看每个记录的 <xref:System.Data.DataRow.RowState%2A> 属性。 （标记为删除的记录的 <xref:System.Data.DataRow.RowState%2A> 为 <xref:System.Data.DataRowState.Deleted>。）或者，您可以创建一个数据集的数据视图，该数据集基于行状态进行筛选，并从该处获取计数属性。

下面的示例演示如何调用 <xref:System.Data.DataRow.Delete%2A> 方法将 `Customers` 表中的第一行标记为已删除：

[!code-csharp[VbRaddataEditing#8](../data-tools/codesnippet/CSharp/edit-data-in-datasets_4.cs)]
[!code-vb[VbRaddataEditing#8](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_4.vb)]

## <a name="determine-if-there-are-changed-rows"></a>确定是否存在更改的行
对数据集中的记录进行更改时，会存储有关这些更改的信息，直到您提交这些更改。 在调用数据集或数据表的 `AcceptChanges` 方法时，或者当调用 TableAdapter 或数据适配器的 `Update` 方法时，可以提交更改。

在每个数据行中跟踪更改的两种方式：

- 每个数据行都包含与其 <xref:System.Data.DataRow.RowState%2A> 相关的信息（例如，<xref:System.Data.DataRowState.Added>、<xref:System.Data.DataRowState.Modified>、<xref:System.Data.DataRowState.Deleted>或 <xref:System.Data.DataRowState.Unchanged>）。

- 每个更改的数据行都包含行的多个版本（<xref:System.Data.DataRowVersion>）、原始版本（在更改之前）和当前版本（更改后）。 在挂起更改（可以响应 <xref:System.Data.DataTable.RowChanging> 事件时）的期间，还可以使用第三个版本（建议的版本）。

如果在 dataset 中进行了更改，则 dataset 的 <xref:System.Data.DataSet.HasChanges%2A> 方法返回 `true`。 确定已更改的行存在后，可以调用 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 的 `GetChanges` 方法来返回一组已更改的行。

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>确定是否已对任何行进行了更改

- 调用数据集的 <xref:System.Data.DataSet.HasChanges%2A> 方法以检查已更改的行。

下面的示例演示如何检查 <xref:System.Data.DataSet.HasChanges%2A> 方法中的返回值，以检测数据集中是否存在名为 `NorthwindDataset1`的已更改行：

[!code-csharp[VbRaddataEditing#12](../data-tools/codesnippet/CSharp/edit-data-in-datasets_5.cs)]
[!code-vb[VbRaddataEditing#12](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_5.vb)]

## <a name="determine-the-type-of-changes"></a>确定更改的类型
还可以通过将值从 <xref:System.Data.DataRowState> 枚举传递到 <xref:System.Data.DataSet.HasChanges%2A> 方法来查看数据集中的更改类型。

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>确定对行所做的更改的类型

- 向 <xref:System.Data.DataSet.HasChanges%2A> 方法传递 <xref:System.Data.DataRowState> 值。

下面的示例演示如何检查名为 `NorthwindDataset1` 的数据集，以确定是否已向其中添加了新行：

[!code-csharp[VbRaddataEditing#13](../data-tools/codesnippet/CSharp/edit-data-in-datasets_6.cs)]
[!code-vb[VbRaddataEditing#13](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_6.vb)]

## <a name="to-locate-rows-that-have-errors"></a>查找有错误的行
使用单个列和数据行时，您可能会遇到错误。 您可以检查 `HasErrors` 属性以确定 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>或 <xref:System.Data.DataRow>中是否存在错误。

1. 检查 `HasErrors` 属性以查看数据集中是否存在任何错误。

2. 如果 `true``HasErrors` 属性，则循环访问表的集合，然后遍历行，以查找包含错误的行。

[!code-csharp[VbRaddataEditing#23](../data-tools/codesnippet/CSharp/edit-data-in-datasets_7.cs)]
[!code-vb[VbRaddataEditing#23](../data-tools/codesnippet/VisualBasic/edit-data-in-datasets_7.vb)]

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
