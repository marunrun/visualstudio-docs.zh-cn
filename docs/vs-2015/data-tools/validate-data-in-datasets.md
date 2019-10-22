---
title: 验证数据集中的数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- DataTable.ColumnChanging
- System.Data.DataTable.ColumnChanging
- System.Data.DataTable.RowChanging
- DataTable.RowChanging
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data validation, datasets
- data validation
- validating data, datasets
- updating datasets, validating data
ms.assetid: 79500596-1e4d-478e-a991-a636fd73a622
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8d42553fbee6de6a89e16716a191db8a3d9fb883
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72621072"
---
# <a name="validate-data-in-datasets"></a>验证数据集中的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

验证数据是确认输入到数据对象中的值是否符合数据集架构中的约束的过程。 验证过程还会确认这些值遵循了已为应用程序建立的规则。 在将更新发送到基础数据库之前对数据进行验证是一种很好的做法。 这可以减少错误，以及应用程序和数据库之间可能出现的往返次数。

 您可以通过在数据集本身中构建验证检查来确认写入数据集的数据是有效的。 无论执行更新的方式是直接由窗体中的控件、在组件内还是以其他方式，数据集都可以检查数据。 由于数据集是你的应用程序的一部分（不同于数据库后端），因此，它是一个用于生成特定于应用程序的验证的逻辑位置。

 向应用程序添加验证的最佳位置是在数据集的分部类文件中。 在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 中，打开**数据集设计器**，然后双击要为其创建验证的列或表。 此操作会自动创建 <xref:System.Data.DataTable.ColumnChanging> 或 <xref:System.Data.DataTable.RowChanging> 事件处理程序。 有关详细信息，请参阅[如何：在列更改过程中验证数据](https://msdn.microsoft.com/library/a2680600-67b6-4a40-a77e-b5bc638281c5)或[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。 有关完整示例，请参阅[演练：向数据集添加验证](https://msdn.microsoft.com/library/09351fab-d670-45e3-b53a-a944eff717e7)。

## <a name="validate-data"></a>验证数据
 可以通过以下方式完成数据集内的验证：

- 通过创建自己的应用程序特定的验证，可以在更改过程中检查单个数据列中的值。  有关详细信息，请参阅[如何：在列更改过程中验证数据](https://msdn.microsoft.com/library/a2680600-67b6-4a40-a77e-b5bc638281c5)。

- 通过创建自己的应用程序特定的验证，可在整个数据行发生更改时将数据检查到值。 有关详细信息，请参阅[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。

- 在数据集的实际架构定义中创建键、唯一约束等。 有关将验证并入架构定义中的详细信息，请参阅[约束 DataColumn 以包含唯一值](https://msdn.microsoft.com/library/8ca21f77-b99a-47a7-a656-7cfd7a1bd9df)。

- 通过设置 <xref:System.Data.DataColumn> 对象的属性，如 <xref:System.Data.DataColumn.MaxLength%2A>、<xref:System.Data.DataColumn.AllowDBNull%2A> 和 <xref:System.Data.DataColumn.Unique%2A>。

  当记录中发生更改时，<xref:System.Data.DataTable> 对象会引发多个事件：

- @No__t_0 和 <xref:System.Data.DataTable.ColumnChanged> 事件在每次更改单个列的过程中和之后引发。 要验证特定列中的更改时，<xref:System.Data.DataTable.ColumnChanging> 事件很有用。 有关建议的更改的信息将作为参数传递到事件。 有关详细信息，请参阅[如何：在列更改过程中验证数据](https://msdn.microsoft.com/library/a2680600-67b6-4a40-a77e-b5bc638281c5)。

- @No__t_0 和 <xref:System.Data.DataTable.RowChanged> 事件会在行中发生更改的过程中和之后引发。 @No__t_0 事件更常见。 它表示行中某个位置发生了更改，但不知道哪个列发生了更改。 有关详细信息，请参阅[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。

  默认情况下，对列的每个更改都将引发四个事件。 第一个是要更改的特定列的 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.ColumnChanged> 事件。 接下来是 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件。 如果对行进行了多项更改，则每次发生更改时都会引发事件。

> [!NOTE]
> 数据行的 <xref:System.Data.DataRow.BeginEdit%2A> 方法关闭每个单个列发生更改后 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件。 在这种情况下，在调用 <xref:System.Data.DataRow.EndEdit%2A> 方法之前，将不会引发事件，而只引发一次 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件。 有关详细信息，请参阅[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

 您选择的事件取决于您希望验证的粒度。 如果在列发生更改时立即捕获错误很重要，请使用 <xref:System.Data.DataTable.ColumnChanging> 事件来生成验证。 否则，请使用 <xref:System.Data.DataTable.RowChanging> 事件，这可能会导致同时捕获几个错误。 此外，如果您的数据是结构化的，以便根据另一列的内容验证一列的值，则在 <xref:System.Data.DataTable.RowChanging> 事件期间执行您的验证。

 当更新记录时，<xref:System.Data.DataTable> 对象将引发事件，您可以在发生更改时和进行更改之后响应这些事件。

 如果你的应用程序使用类型化数据集，则可以创建强类型的事件处理程序。 这将添加四个可以为其创建处理程序的其他类型事件： `dataTableNameRowChanging`、`dataTableNameRowChanged`、`dataTableNameRowDeleting` 和 `dataTableNameRowDeleted`。 这些类型化的事件处理程序传递一个参数，该参数包含表的列名，使代码更易于编写和读取。

## <a name="data-update-events"></a>数据更新事件

|Event — 事件|描述|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|列中的值正在更改。 事件向您传递行和列以及建议的新值。|
|<xref:System.Data.DataTable.ColumnChanged>|列中的值已更改。 事件向您传递行和列以及建议的值。|
|<xref:System.Data.DataTable.RowChanging>|对 <xref:System.Data.DataRow> 对象所做的更改将提交回数据集。 如果尚未调用 <xref:System.Data.DataRow.BeginEdit%2A> 方法，则在引发 <xref:System.Data.DataTable.ColumnChanging> 事件之后，将对列的每次更改引发 <xref:System.Data.DataTable.RowChanging> 事件。 如果在进行更改之前调用了 <xref:System.Data.DataRow.BeginEdit%2A>，则只有在调用 <xref:System.Data.DataRow.EndEdit%2A> 方法时，才会引发 <xref:System.Data.DataTable.RowChanging> 事件。<br /><br /> 事件将行传递给您，并提供一个值，指示正在执行的操作类型（更改、插入等）。|
|<xref:System.Data.DataTable.RowChanged>|已更改行。 事件将行传递给您，并提供一个值，指示正在执行的操作类型（更改、插入等）。|
|<xref:System.Data.DataTable.RowDeleting>|正在删除行。 事件将行传递给您，并提供一个指示正在执行的操作类型的值。|
|<xref:System.Data.DataTable.RowDeleted>|已删除行。 事件将行传递给您，并提供一个指示正在执行的操作类型的值。|

 更新过程中会引发 <xref:System.Data.DataTable.ColumnChanging>、<xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowDeleting> 事件。 您可以使用这些事件来验证数据或执行其他类型的处理。 由于在这些事件期间正在进行更新，因此你可以通过引发异常来取消更新，这会阻止更新完成。

 @No__t_0、<xref:System.Data.DataTable.RowChanged> 和 <xref:System.Data.DataTable.RowDeleted> 事件是更新成功完成后引发的通知事件。 如果希望根据成功的更新执行进一步的操作，这些事件很有用。

## <a name="validate-data-during-column-changes"></a>在列更改过程中验证数据

> [!NOTE]
> **数据集设计器**创建一个可在其中将验证逻辑添加到数据集的分部类。 设计器生成的数据集不会删除或更改分部类中的任何代码。

 当数据列中的值更改时，可以通过响应 <xref:System.Data.DataTable.ColumnChanging> 事件来验证数据。 当引发时，此事件传递一个事件参数（<xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A>），该参数包含当前列所建议的值。 根据 `e.ProposedValue` 的内容，您可以：

- 不执行任何操作，接受建议的值。

- 通过在列更改事件处理程序中设置列错误（<xref:System.Data.DataRow.SetColumnError%2A>）来拒绝建议的值。

- （可选）使用 <xref:System.Windows.Forms.ErrorProvider> 控件向用户显示一条错误消息。 有关详细信息，请参阅[ErrorProvider 组件](https://msdn.microsoft.com/library/c0f2e231-c5c9-413d-a507-75af2db499b6)。

  还可以在 <xref:System.Data.DataTable.RowChanging> 事件期间执行验证。 有关详细信息，请参阅[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。

## <a name="validate-data-during-row-changes"></a>在行更改过程中验证数据
 您可以编写代码以验证您要验证的每个列是否包含满足您的应用程序要求的数据。 为此，请将列设置为，以指示如果建议的值不可接受，则该列包含错误。 下面的示例在 `Quantity` 列小于0时设置列错误。 行更改事件处理程序应类似于以下示例。

#### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>在行发生更改时验证数据（Visual Basic）

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。

2. 双击要验证的表的标题栏。 此操作会在数据集的分部类文件中自动创建 <xref:System.Data.DataTable> 的 <xref:System.Data.DataTable.RowChanging> 事件处理程序。

    > [!TIP]
    > 双击表名称的左侧，创建行更改事件处理程序。 如果双击表名，则可以对其进行编辑。

     [!code-vb[VbRaddataValidating#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataValidating/VB/NorthwindDataSet.vb#3)]

#### <a name="to-validate-data-when-a-row-changes-c"></a>在行发生更改时验证数据（C#）

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。

2. 双击要验证的表的标题栏。 此操作创建 <xref:System.Data.DataTable> 的分部类文件。

    > [!NOTE]
    > **数据集设计器**不会自动为 <xref:System.Data.DataTable.RowChanging> 事件创建事件处理程序。 您必须创建一个方法来处理 <xref:System.Data.DataTable.RowChanging> 事件，并运行代码以在表的初始化方法中挂接该事件。

3. 将以下代码复制到分部类中：

    ```
    public override void EndInit()
    {
        base.EndInit();
        Order_DetailsRowChanging += TestRowChangeEvent;
    }

    public void TestRowChangeEvent(object sender, Order_DetailsRowChangeEvent e)
    {
        if ((short)e.Row.Quantity <= 0)
        {
            e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
        }
        else
        {
            e.Row.SetColumnError("Quantity", "");
        }
    }
    ```

## <a name="to-retrieve-changed-rows"></a>检索已更改的行
 数据表中的每行都有一个 <xref:System.Data.DataRow.RowState%2A> 属性，该属性通过使用 <xref:System.Data.DataRowState> 枚举中的值跟踪该行的当前状态。 您可以通过调用 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 的 `GetChanges` 方法，从数据集或数据表返回已更改的行。 可以通过调用数据集的 <xref:System.Data.DataSet.HasChanges%2A> 方法在调用 `GetChanges` 之前验证是否存在更改。 有关 <xref:System.Data.DataSet.HasChanges%2A> 的详细信息，请参阅[如何：检查已更改的行](https://msdn.microsoft.com/library/af160d20-472b-4c13-8f15-75480c39a653)。

> [!NOTE]
> 将更改提交到数据集或数据表（通过调用 <xref:System.Data.DataSet.AcceptChanges%2A> 方法）后，`GetChanges` 方法不会返回任何数据。 如果应用程序需要处理已更改的行，则必须在调用 `AcceptChanges` 方法之前处理这些更改。

 如果调用数据集或数据表的 <xref:System.Data.DataSet.GetChanges%2A> 方法，将返回仅包含已更改的记录的新数据集或数据表。 如果要获取特定记录（例如，仅新记录或仅修改记录），可以将 <xref:System.Data.DataRowState> 枚举中的值作为参数传递给 `GetChanges` 方法。

 使用 <xref:System.Data.DataRowVersion> 枚举访问行的不同版本（例如，在处理行之前在行中的原始值）。

#### <a name="to-get-all-changed-records-from-a-dataset"></a>从数据集中获取所有已更改的记录

- 调用数据集的 <xref:System.Data.DataSet.GetChanges%2A> 方法。

     下面的示例创建一个名为 `changedRecords` 的新数据集，并使用另一个名为 `dataSet1` 的数据集的所有已更改记录填充它。

     [!code-csharp[VbRaddataEditing#14](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#14)]
     [!code-vb[VbRaddataEditing#14](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#14)]

#### <a name="to-get-all-changed-records-from-a-data-table"></a>从数据表获取所有更改的记录

- 调用 DataTable 的 <xref:System.Data.DataTable.GetChanges%2A> 方法。

     下面的示例创建一个名为 `changedRecordsTable` 的新数据表，并使用另一个名为 `dataTable1` 的数据表中的所有已更改记录填充该数据表。

     [!code-csharp[VbRaddataEditing#15](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#15)]
     [!code-vb[VbRaddataEditing#15](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#15)]

#### <a name="to-get-all-records-that-have-a-specific-row-state"></a>获取具有特定行状态的所有记录

- 调用数据集或数据表的 `GetChanges` 方法，并以参数的形式传递 <xref:System.Data.DataRowState> 枚举值。

     下面的示例演示如何创建一个名为 `addedRecords` 的新数据集，并仅使用已添加到 `dataSet1` 数据集的记录来填充它。

     [!code-csharp[VbRaddataEditing#16](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#16)]
     [!code-vb[VbRaddataEditing#16](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#16)]

- 下面的示例演示如何返回最近添加到 `Customers` 表中的所有记录：

     [!code-csharp[VbRaddataEditing#17](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#17)]
     [!code-vb[VbRaddataEditing#17](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#17)]

## <a name="access-the-original-version-of-a-datarow"></a>访问 DataRow 的原始版本
 对数据行进行更改时，数据集将保留该行的原始（<xref:System.Data.DataRowVersion>）和新的（<xref:System.Data.DataRowVersion>）版本。 例如，在调用 `AcceptChanges` 方法之前，应用程序可以访问记录的不同版本（如 <xref:System.Data.DataRowVersion> 枚举中的定义）并相应地处理更改。

> [!NOTE]
> 行的不同版本仅在已编辑或在调用 `AcceptChanges` 方法之前存在。 调用 `AcceptChanges` 方法后，当前版本和原始版本是相同的。

 将 <xref:System.Data.DataRowVersion> 值与列索引（或字符串形式的列名称）一起传递将从该列的特定行版本返回值。 在 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.ColumnChanged> 事件期间，会标识已更改的列。 这是检查不同行版本以进行验证的好时机。 但是，如果您暂时挂起了约束，则不会引发这些事件，您将需要以编程方式标识哪些列已更改。 为此，可以循环访问 <xref:System.Data.DataTable.Columns%2A> 集合，并比较不同的 <xref:System.Data.DataRowVersion> 值。

#### <a name="to-get-the-original-version-of-a-record"></a>获取记录的原始版本

- 通过传入要返回的行的 <xref:System.Data.DataRowVersion> 访问列的值。

     下面的示例演示如何使用 <xref:System.Data.DataRowVersion> 值获取 <xref:System.Data.DataRow> 中 `CompanyName` 字段的原始值：

     [!code-csharp[VbRaddataEditing#21](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#21)]
     [!code-vb[VbRaddataEditing#21](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#21)]

## <a name="access-the-current-version-of-a-datarow"></a>访问 DataRow 的当前版本

#### <a name="to-get-the-current-version-of-a-record"></a>获取记录的当前版本

- 访问列的值，然后向该索引添加一个参数，用于指示要返回的行的版本。

     下面的示例演示如何使用 <xref:System.Data.DataRowVersion> 值获取 <xref:System.Data.DataRow> 中 `CompanyName` 字段的当前值：

     [!code-csharp[VbRaddataEditing#22](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#22)]
     [!code-vb[VbRaddataEditing#22](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#22)]

## <a name="see-also"></a>请参阅

- [如何：在 Windows 窗体 DataGridView 控件中验证数据](https://msdn.microsoft.com/library/d10aef35-701e-4a3c-a684-2a2ed1aeaca6)
- [如何：使用 Windows 窗体 ErrorProvider 组件显示窗体验证的错误图标](https://msdn.microsoft.com/library/3b681a32-9db4-497b-a34b-34980eabee46)