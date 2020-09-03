---
title: 编辑数据集中的数据 |Microsoft Docs
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
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 699ee9b6e7a68c6a79f7f7dac526127206e8aa42
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672405"
---
# <a name="edit-data-in-datasets"></a>编辑数据集中的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑数据表中的数据与编辑任何数据库的表中的数据非常类似。 此过程可能包括插入、更新和删除表中的记录。 在数据绑定窗体中，可以指定哪些字段是用户可编辑的字段。 在这些情况下，数据绑定基础结构将处理所有更改跟踪，以便以后可以将更改发送回数据库。 如果以编程方式对数据进行编辑，并且想要将这些更改发送回数据库，则必须使用执行更改跟踪的对象和方法。

 除了更改实际数据之外，您还可以查询 <xref:System.Data.DataTable> 以返回特定的数据行。 例如，您可以查询单个行、特定版本的行 (原始和建议) 、已更改的行或有错误的行。

## <a name="to-edit-rows-in-a-dataset"></a>编辑数据集中的行
 若要编辑中的现有行 <xref:System.Data.DataTable> ，需要找到 <xref:System.Data.DataRow> 要编辑的，然后将更新后的值分配给所需的列。

 如果您不知道要编辑的行的索引，请使用 `FindBy` 方法按主键进行搜索：

 [!code-csharp[VbRaddataEditing#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#3)]
 [!code-vb[VbRaddataEditing#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#3)]

 如果知道行索引，则可以访问和编辑行，如下所示：

 [!code-csharp[VbRaddataEditing#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#5)]
 [!code-vb[VbRaddataEditing#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#5)]

## <a name="to-insert-new-rows-into-a-dataset"></a>向数据集插入新行
 使用数据绑定控件的应用程序通常通过[BindingNavigator 控件](https://msdn.microsoft.com/library/18c1e2a5-9834-40d3-9b2e-2b545e4e769e)上的 "**添加新**项" 按钮来添加新记录。

 若要将新记录手动添加到数据集，请通过对 DataTable 调用方法来创建新的数据行。 然后，将该行添加到 <xref:System.Data.DataRow> 集合 (的 <xref:System.Data.DataTable.Rows%2A>) <xref:System.Data.DataTable> ：

 [!code-csharp[VbRaddataEditing#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#1)]
 [!code-vb[VbRaddataEditing#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#1)]

 为了保留数据集将更新发送到数据源所需的信息，请使用 <xref:System.Data.DataRow.Delete%2A> 方法删除数据表中的行。 例如，如果应用程序使用 TableAdapter (或 <xref:System.Data.Common.DataAdapter>) ，则 TableAdapter 的 `Update` 方法会删除数据库中具有 <xref:System.Data.DataRow.RowState%2A> 的行 <xref:System.Data.DataRowState> 。

 如果你的应用程序不需要将更新发送回数据源，则可以通过直接访问数据行集合 () 来删除记录 <xref:System.Data.DataRowCollection.Remove%2A> 。

#### <a name="to-delete-records-from-a-data-table"></a>删除数据表中的记录

- 调用的 <xref:System.Data.DataRow.Delete%2A> 方法 <xref:System.Data.DataRow> 。

     此方法不会以物理方式删除记录。 相反，它会将记录标记为要删除。

    > [!NOTE]
    > 如果获取的计数属性 <xref:System.Data.DataRowCollection> ，则生成的计数将包含已标记为要删除的记录。 若要获取未标记为要删除的记录的准确计数，可以循环遍历 <xref:System.Data.DataRow.RowState%2A> 每个记录的属性的集合。 标记为删除 (记录的 <xref:System.Data.DataRow.RowState%2A> <xref:System.Data.DataRowState> ) 或者，你可以创建一个数据集的数据视图，该数据集基于行状态进行筛选，并从该处获取计数属性。

     下面的示例演示如何调用 <xref:System.Data.DataRow.Delete%2A> 方法，将表中的第一行标记 `Customers` 为已删除：

     [!code-csharp[VbRaddataEditing#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#8)]
     [!code-vb[VbRaddataEditing#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#8)]

## <a name="determine-if-there-are-changed-rows"></a>确定是否存在更改的行
 对数据集中的记录进行更改时，会存储有关这些更改的信息，直到您提交这些更改。 在调用 `AcceptChanges` 数据集或数据表的方法时，或者当调用 `Update` TableAdapter 或数据适配器的方法时，将提交更改。

 在每个数据行中跟踪更改的两种方式：

- 每个数据行都包含与 (有关的信息 <xref:System.Data.DataRow.RowState%2A> ，例如，、 <xref:System.Data.DataRowState> <xref:System.Data.DataRowState> 、 <xref:System.Data.DataRowState> 或 <xref:System.Data.DataRowState>) 。

- 每个更改的数据行都包含该行 () 的多个版本 <xref:System.Data.DataRowVersion> 、在更改) 之前的原始版本 (，以及 (更改后) 当前版本。 当更改处于挂起状态时 (可以响应 <xref:System.Data.DataTable.RowChanging> 事件) 的时间，还可以使用第三个版本（建议的版本）。

  <xref:System.Data.DataSet.HasChanges%2A> `true` 如果在数据集中进行了更改，则 dataset 的方法将返回。 确定已更改的行存在后，可以调用 `GetChanges` 或的方法 <xref:System.Data.DataSet> <xref:System.Data.DataTable> 来返回一组已更改的行。 有关详细信息，请参阅 [如何：检索已更改的行](https://msdn.microsoft.com/library/6ff0cbd0-5253-48e7-888a-144d56c2e0a9)。

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>确定是否已对任何行进行了更改

- 调用 <xref:System.Data.DataSet.HasChanges%2A> 数据集的方法以检查已更改的行。

     下面的示例演示如何检查方法中的返回值 <xref:System.Data.DataSet.HasChanges%2A> ，以检测数据集中是否存在任何已更改的行 `NorthwindDataset1` ：

     [!code-csharp[VbRaddataEditing#12](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#12)]
     [!code-vb[VbRaddataEditing#12](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#12)]

## <a name="determine-the-type-of-changes"></a>确定更改的类型
 还可以通过将枚举中的值传递给方法来查看数据集中的更改类型 <xref:System.Data.DataRowState> <xref:System.Data.DataSet.HasChanges%2A> 。

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>确定对行所做的更改的类型

- <xref:System.Data.DataRowState>向方法传递值 <xref:System.Data.DataSet.HasChanges%2A> 。

     下面的示例演示如何检查名为的数据集 `NorthwindDataset1` ，以确定是否已向其中添加了新行：

     [!code-csharp[VbRaddataEditing#13](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#13)]
     [!code-vb[VbRaddataEditing#13](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#13)]

## <a name="to-locate-rows-that-have-errors"></a>查找有错误的行
 使用单个列和数据行时，您可能会遇到错误。 可以通过检查 `HasErrors` 属性来确定、或中是否存在错误 <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow> 。

1. 检查 `HasErrors` 属性以查看数据集中是否存在任何错误。

2. 如果 `HasErrors` 属性为 `true` ，则循环访问表的集合，然后循环访问行，以便查找出错的行。

     [!code-csharp[VbRaddataEditing#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#23)]
     [!code-vb[VbRaddataEditing#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#23)]
