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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7cbc9519c86b2bf4967e567b29355eb6d8a176a4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699772"
---
# <a name="edit-data-in-datasets"></a>编辑数据集中的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑任何数据库中的表中的数据一样编辑数据的表中的数据。 过程可以包括插入、 更新和删除表中的记录。 在数据绑定窗体中，可以指定哪些字段是用户可编辑。 在这些情况下，数据绑定基础结构可处理所有更改跟踪，以便所做的更改可以发送回数据库更高版本。 如果以编程方式对数据进行编辑，并且你想要将这些更改发送回数据库，必须使用的对象和为您做的更改跟踪的方法。  
  
 除了更改实际数据，还可以查询<xref:System.Data.DataTable>返回特定的数据行。 例如，您可能会查询各个行、 行 （原始和建议） 的特定版本，已更改的行或有错误的行。  
  
## <a name="to-edit-rows-in-a-dataset"></a>若要编辑数据集中的行  
 若要编辑中的现有行<xref:System.Data.DataTable>，则需查找<xref:System.Data.DataRow>你想要编辑，然后将更新后的值分配给所需的列。  
  
 如果不知道的行的索引，你想要编辑，请使用`FindBy`方法搜索的主键：  
  
 [!code-csharp[VbRaddataEditing#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#3)]
 [!code-vb[VbRaddataEditing#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#3)]  
  
 如果您知道的行索引，您可以访问和编辑的行，如下所示：  
  
 [!code-csharp[VbRaddataEditing#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#5)]
 [!code-vb[VbRaddataEditing#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#5)]  
  
## <a name="to-insert-new-rows-into-a-dataset"></a>若要将新行插入到数据集  
 通常使用数据绑定控件的应用程序添加新记录通过**新添**按钮[BindingNavigator 控件](https://msdn.microsoft.com/library/18c1e2a5-9834-40d3-9b2e-2b545e4e769e)。  
  
 若要手动将新记录添加到数据集，通过调用 DataTable 方法创建新的数据行。 然后向其中添加行<xref:System.Data.DataRow>集合 (<xref:System.Data.DataTable.Rows%2A>) 的<xref:System.Data.DataTable>:  
  
 [!code-csharp[VbRaddataEditing#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#1)]
 [!code-vb[VbRaddataEditing#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#1)]  
  
 若要保留数据集将更新发送到数据源所需的信息，请使用<xref:System.Data.DataRow.Delete%2A>方法删除数据表中的行。 例如，如果你的应用程序使用 TableAdapter (或<xref:System.Data.Common.DataAdapter>)，TableAdapter`Update`方法中删除数据库中具有的行<xref:System.Data.DataRow.RowState%2A>的<xref:System.Data.DataRowState>。  
  
 如果你的应用程序并不需要将更新发送回数据源，然后就可以通过直接访问数据行集合中删除记录 (<xref:System.Data.DataRowCollection.Remove%2A>)。  
  
#### <a name="to-delete-records-from-a-data-table"></a>若要从数据表中删除记录  
  
- 调用<xref:System.Data.DataRow.Delete%2A>方法的<xref:System.Data.DataRow>。  
  
     此方法不会以物理方式删除记录。 相反，它将标记为删除的记录。  
  
    > [!NOTE]
    > 如果收到的 count 属性<xref:System.Data.DataRowCollection>，在生成的计数包括已标记为删除的记录。 若要获取不会将标记为删除的记录的精确计数，可以循环访问集合，查看<xref:System.Data.DataRow.RowState%2A>每个记录属性。 (标记为删除的记录具有<xref:System.Data.DataRow.RowState%2A>的<xref:System.Data.DataRowState>。)或者，可以创建数据视图的筛选器根据行状态的数据集，并从那里获取的 count 属性。  
  
     下面的示例演示如何调用<xref:System.Data.DataRow.Delete%2A>方法将标记中的第一行`Customers`表为已删除：  
  
     [!code-csharp[VbRaddataEditing#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#8)]
     [!code-vb[VbRaddataEditing#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#8)]  
  
## <a name="determine-if-there-are-changed-rows"></a>确定是否已更改的行  
 当在数据集中的记录进行更改时，将它们提交之前将存储有关这些更改的信息。 在调用时提交所做的更改`AcceptChanges`方法的数据集或数据的表，或在调用时`Update`TableAdapter 或数据适配器的方法。  
  
 更改是在每个数据行中的跟踪两种方法：  
  
- 每个数据行包含与它的相关信息<xref:System.Data.DataRow.RowState%2A>(例如， <xref:System.Data.DataRowState>， <xref:System.Data.DataRowState>， <xref:System.Data.DataRowState>，或<xref:System.Data.DataRowState>)。  
  
- 每个已更改的数据行包含该行的多个版本 (<xref:System.Data.DataRowVersion>)，（更改） 之前, 的原始版本和 （之后的更改） 的当前版本。 期间挂起的更改时 (可以作出响应的时间<xref:System.Data.DataTable.RowChanging>事件)、 第三个版本 — 提议的版本，也可以。
  
  <xref:System.Data.DataSet.HasChanges%2A>数据集的方法将返回`true`如果在数据集中进行了更改。 确定已更改的行存在之后, 可以调用`GetChanges`方法<xref:System.Data.DataSet>或<xref:System.Data.DataTable>返回一组已更改的行。 有关详细信息，请参阅[如何：检索已更改的行](https://msdn.microsoft.com/library/6ff0cbd0-5253-48e7-888a-144d56c2e0a9)。  
  
#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>若要确定是否已对任何行进行了更改  
  
- 调用<xref:System.Data.DataSet.HasChanges%2A>方法要检查的数据集已更改的行。  
  
     下面的示例演示如何检查的返回值<xref:System.Data.DataSet.HasChanges%2A>方法来检测中名为的数据集是否有任何已更改的行`NorthwindDataset1`:  
  
     [!code-csharp[VbRaddataEditing#12](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#12)]
     [!code-vb[VbRaddataEditing#12](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#12)]  
  
## <a name="determine-the-type-of-changes"></a>确定更改的类型  
 您还可以检查以查看哪种类型的更改中进行了数据集通过将值从传递<xref:System.Data.DataRowState>枚举<xref:System.Data.DataSet.HasChanges%2A>方法。  
  
#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>若要确定哪种类型的更改已对某行  
  
- 传递<xref:System.Data.DataRowState>值设为<xref:System.Data.DataSet.HasChanges%2A>方法。  
  
     下面的示例演示如何检查名为的数据集`NorthwindDataset1`以确定是否向其添加了任何新行：  
  
     [!code-csharp[VbRaddataEditing#13](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#13)]
     [!code-vb[VbRaddataEditing#13](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#13)]  
  
## <a name="to-locate-rows-that-have-errors"></a>若要查找具有错误的行  
 当使用单个列和行数据，可能会遇到错误。 你可以检查`HasErrors`属性来确定是否存在错误<xref:System.Data.DataSet>， <xref:System.Data.DataTable>，或<xref:System.Data.DataRow>。  
  
1. 检查`HasErrors`属性以查看数据集内是否有任何错误。  
  
2. 如果`HasErrors`属性是`true`，循环访问表的集合，然后通过行，以查找具有错误的行。  
  
     [!code-csharp[VbRaddataEditing#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#23)]
     [!code-vb[VbRaddataEditing#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#23)]
