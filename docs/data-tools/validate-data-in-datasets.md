---
title: 验证数据集中的数据
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DataTable.ColumnChanging
- System.Data.DataTable.ColumnChanging
- System.Data.DataTable.RowChanging
- DataTable.RowChanging
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data validation, datasets
- data validation
- validating data, datasets
- updating datasets, validating data
ms.assetid: 79500596-1e4d-478e-a991-a636fd73a622
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 80f258e87bd7bd197460d5ff9ab29b6964347f7c
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925420"
---
# <a name="validate-data-in-datasets"></a>验证数据集中的数据
验证数据是确认输入到数据对象中的值是否符合数据集架构中的约束的过程。 验证过程还会确认这些值遵循了已为应用程序建立的规则。 在将更新发送到基础数据库之前对数据进行验证是一种很好的做法。 这可以减少错误, 以及应用程序和数据库之间可能出现的往返次数。

您可以通过在数据集本身中构建验证检查来确认写入数据集的数据是有效的。 无论执行更新的方式是直接由窗体中的控件、在组件内还是以其他方式, 数据集都可以检查数据。 由于数据集是你的应用程序的一部分 (不同于数据库后端), 因此, 它是一个用于生成特定于应用程序的验证的逻辑位置。

向应用程序添加验证的最佳位置是在数据集的分部类文件中。 在[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]或[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]中打开**数据集设计器**, 然后双击要为其创建验证的列或表。 此操作会自动创建<xref:System.Data.DataTable.ColumnChanging>或<xref:System.Data.DataTable.RowChanging>事件处理程序。

## <a name="validate-data"></a>验证数据
数据集内的验证通过以下方式完成:

- 通过创建自己的应用程序特定的验证, 可以在更改过程中检查单个数据列中的值。 有关详细信息，请参阅[如何：在列更改](validate-data-in-datasets.md)过程中验证数据。

- 通过创建自己的应用程序特定的验证, 可在整个数据行发生更改时将数据检查到值。 有关详细信息，请参阅[如何：在行更改](validate-data-in-datasets.md)过程中验证数据。

- 在数据集的实际架构定义中创建键、唯一约束等。

- 通过设置<xref:System.Data.DataColumn>对象的属性, <xref:System.Data.DataColumn.MaxLength%2A>如、 <xref:System.Data.DataColumn.AllowDBNull%2A>和<xref:System.Data.DataColumn.Unique%2A>。

当记录中发生更改时<xref:System.Data.DataTable> , 对象会引发多个事件:

- <xref:System.Data.DataTable.ColumnChanging> 和<xref:System.Data.DataTable.ColumnChanged>事件在每次更改单个列的过程中和之后引发。 要<xref:System.Data.DataTable.ColumnChanging>验证特定列中的更改时, 事件很有用。 有关建议的更改的信息将作为参数传递到事件。
- <xref:System.Data.DataTable.RowChanging> 和<xref:System.Data.DataTable.RowChanged>事件是在行中的任何更改前后引发的。 <xref:System.Data.DataTable.RowChanging>事件更常见。 它表示行中某个位置发生了更改, 但不知道哪个列发生了更改。

默认情况下, 对列的每个更改都将引发四个事件。 第一个是要<xref:System.Data.DataTable.ColumnChanging>更改<xref:System.Data.DataTable.ColumnChanged>的特定列的和事件。 接下来是<xref:System.Data.DataTable.RowChanging>和<xref:System.Data.DataTable.RowChanged>事件。 如果对行进行了多项更改, 则每次发生更改时都会引发事件。

> [!NOTE]
> 数据行的<xref:System.Data.DataRow.BeginEdit%2A>方法在每个单个列<xref:System.Data.DataTable.RowChanged>发生更改后<xref:System.Data.DataTable.RowChanging>关闭和事件。 在这种情况下, 在调用<xref:System.Data.DataRow.EndEdit%2A>方法之前, <xref:System.Data.DataTable.RowChanging>如果仅引发一次和<xref:System.Data.DataTable.RowChanged>事件, 则不会引发事件。 有关详细信息, 请参阅[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

您选择的事件取决于您希望验证的粒度。 如果在列发生更改时立即捕获错误很重要, 则使用<xref:System.Data.DataTable.ColumnChanging>事件生成验证。 否则, 请使用<xref:System.Data.DataTable.RowChanging>事件, 这可能会导致同时捕获几个错误。 此外, 如果您的数据是结构化的, 以便根据另一列的内容来验证一个列的值, 则在该<xref:System.Data.DataTable.RowChanging>事件期间执行验证。

当更新记录时, <xref:System.Data.DataTable>对象会引发事件, 您可以在发生更改时和进行更改之后响应这些事件。

如果你的应用程序使用类型化数据集, 则可以创建强类型的事件处理程序。 这将添加四个可以为其创建处理程序的其他`dataTableNameRowChanging`类型`dataTableNameRowChanged`事件`dataTableNameRowDeleting`:、 `dataTableNameRowDeleted`、和。 这些类型化的事件处理程序传递一个参数, 该参数包含表的列名, 使代码更易于编写和读取。

## <a name="data-update-events"></a>数据更新事件

|Event|描述|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|列中的值正在更改。 事件向您传递行和列以及建议的新值。|
|<xref:System.Data.DataTable.ColumnChanged>|列中的值已更改。 事件向您传递行和列以及建议的值。|
|<xref:System.Data.DataTable.RowChanging>|对<xref:System.Data.DataRow>对象所做的更改将提交回数据集。 如果未调用<xref:System.Data.DataRow.BeginEdit%2A>方法<xref:System.Data.DataTable.RowChanging> , 则在引发<xref:System.Data.DataTable.ColumnChanging>事件后, 将对列的每次更改引发事件。 如果在进行<xref:System.Data.DataRow.BeginEdit%2A>更改之前调用<xref:System.Data.DataTable.RowChanging> , 则<xref:System.Data.DataRow.EndEdit%2A>仅在调用方法时引发事件。<br /><br /> 事件将行传递给您, 并提供一个值, 指示正在执行的操作类型 (更改、插入等)。|
|<xref:System.Data.DataTable.RowChanged>|已更改行。 事件将行传递给您, 并提供一个值, 指示正在执行的操作类型 (更改、插入等)。|
|<xref:System.Data.DataTable.RowDeleting>|正在删除行。 事件将行传递给您, 并提供一个指示正在执行的操作类型的值。|
|<xref:System.Data.DataTable.RowDeleted>|已删除行。 事件将行传递给您, 并提供一个指示正在执行的操作类型的值。|

在更新<xref:System.Data.DataTable.RowChanging>过程中<xref:System.Data.DataTable.RowDeleting>会引发、和事件。<xref:System.Data.DataTable.ColumnChanging> 您可以使用这些事件来验证数据或执行其他类型的处理。 由于在这些事件期间正在进行更新, 因此你可以通过引发异常来取消更新, 这会阻止更新完成。

<xref:System.Data.DataTable.ColumnChanged>、和事件<xref:System.Data.DataTable.RowDeleted>是更新成功完成后引发的通知事件。 <xref:System.Data.DataTable.RowChanged> 如果希望根据成功的更新执行进一步的操作, 这些事件很有用。

## <a name="validate-data-during-column-changes"></a>在列更改过程中验证数据

> [!NOTE]
> **数据集设计器**创建一个可在其中将验证逻辑添加到数据集的分部类。 设计器生成的数据集不会删除或更改分部类中的任何代码。

当数据列中的值更改时, 可以通过响应<xref:System.Data.DataTable.ColumnChanging>事件来验证数据。 当引发时, 此事件传递一个事件参数<xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A>(), 该参数包含当前列所建议的值。 根据的内容`e.ProposedValue`, 您可以:

- 不执行任何操作, 接受建议的值。

- 通过在列更改事件处理程序中设置列<xref:System.Data.DataRow.SetColumnError%2A>错误 (), 拒绝建议的值。

- 选择性地使用<xref:System.Windows.Forms.ErrorProvider>控件向用户显示错误消息。 有关详细信息，请参阅 [ErrorProvider 组件](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)。

还可以在<xref:System.Data.DataTable.RowChanging>事件期间执行验证。

## <a name="validate-data-during-row-changes"></a>在行更改过程中验证数据
您可以编写代码以验证您要验证的每个列是否包含满足您的应用程序要求的数据。 为此, 请将列设置为, 以指示如果建议的值不可接受, 则该列包含错误。 下面的示例在`Quantity`列等于或小于0时设置列错误。 行更改事件处理程序应类似于以下示例。

### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>在行发生更改时验证数据 (Visual Basic)

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参见[演练：在数据集设计器](walkthrough-creating-a-dataset-with-the-dataset-designer.md)中创建数据集。

2. 双击要验证的表的标题栏。 此操作会在数据<xref:System.Data.DataTable.RowChanging>集的分部类<xref:System.Data.DataTable>文件中自动创建的事件处理程序。

    > [!TIP]
    > 双击表名称的左侧, 创建行更改事件处理程序。 如果双击表名, 则可以对其进行编辑。

     [!code-vb[VbRaddataValidating#3](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_1.vb)]

### <a name="to-validate-data-when-a-row-changes-c"></a>在行发生更改时验证数据 (C#)

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参见[演练：在数据集设计器](walkthrough-creating-a-dataset-with-the-dataset-designer.md)中创建数据集。

2. 双击要验证的表的标题栏。 此操作为<xref:System.Data.DataTable>创建的分部类文件。

    > [!NOTE]
    > **数据集设计器**不会自动为<xref:System.Data.DataTable.RowChanging>事件创建事件处理程序。 您必须创建用于处理事件的<xref:System.Data.DataTable.RowChanging>方法, 并运行代码以在表的初始化方法中挂接该事件。

3. 将以下代码复制到分部类中:

    ```csharp
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
数据表中的每一行都有一个<xref:System.Data.DataRow.RowState%2A>属性, 该属性使用<xref:System.Data.DataRowState>枚举中的值跟踪该行的当前状态。 您可以通过调用`GetChanges` <xref:System.Data.DataSet>或<xref:System.Data.DataTable>的方法, 从数据集或数据表返回已更改的行。 可以通过`GetChanges` <xref:System.Data.DataSet.HasChanges%2A>调用 dataset 的方法来验证在调用之前是否存在更改。

> [!NOTE]
> 将更改提交到数据集或数据表后 (通过调用<xref:System.Data.DataSet.AcceptChanges%2A>方法), 该`GetChanges`方法不返回任何数据。 如果应用程序需要处理已更改的行, 则必须在调用`AcceptChanges`方法之前处理这些更改。

调用数据集或数据表的方法将返回仅包含已更改的记录的新数据集或数据表。<xref:System.Data.DataSet.GetChanges%2A> 如果要获取特定记录 (例如, 仅新记录或仅修改记录), 可以将<xref:System.Data.DataRowState>枚举中的值作为参数传递`GetChanges`给方法。

<xref:System.Data.DataRowVersion>使用枚举可以访问行的不同版本 (例如, 在处理行之前在行中的原始值)。

### <a name="to-get-all-changed-records-from-a-dataset"></a>从数据集中获取所有已更改的记录

- 调用数据集的方法。<xref:System.Data.DataSet.GetChanges%2A>

     下面的示例创建一个名`changedRecords`为的新数据集, 并将其与另一个名`dataSet1`为的数据集的所有已更改记录一起填充。

     [!code-csharp[VbRaddataEditing#14](../data-tools/codesnippet/CSharp/validate-data-in-datasets_2.cs)]
     [!code-vb[VbRaddataEditing#14](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_2.vb)]

### <a name="to-get-all-changed-records-from-a-data-table"></a>从数据表获取所有更改的记录

- 调用 DataTable 的方法。 <xref:System.Data.DataTable.GetChanges%2A>

     下面的示例将创建一个名`changedRecordsTable`为的新数据表, 并使用另一个名`dataTable1`为的数据表中已更改的所有记录填充该数据表。

     [!code-csharp[VbRaddataEditing#15](../data-tools/codesnippet/CSharp/validate-data-in-datasets_3.cs)]
     [!code-vb[VbRaddataEditing#15](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_3.vb)]

### <a name="to-get-all-records-that-have-a-specific-row-state"></a>获取具有特定行状态的所有记录

- 调用数据集或数据表的<xref:System.Data.DataRowState> 方法,并以参数的形式传递枚举值。`GetChanges`

     下面的示例演示如何创建一个名`addedRecords`为的新数据集, 并使用已添加到该数据集的`dataSet1`记录来填充它。

     [!code-csharp[VbRaddataEditing#16](../data-tools/codesnippet/CSharp/validate-data-in-datasets_4.cs)]
     [!code-vb[VbRaddataEditing#16](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_4.vb)]

     下面的示例演示如何返回最近添加到表中的`Customers`所有记录:

     [!code-csharp[VbRaddataEditing#17](../data-tools/codesnippet/CSharp/validate-data-in-datasets_5.cs)]
     [!code-vb[VbRaddataEditing#17](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_5.vb)]

## <a name="access-the-original-version-of-a-datarow"></a>访问 DataRow 的原始版本
对数据行进行更改时, 数据集将保留该行的原始 (<xref:System.Data.DataRowVersion.Original>) 和新 (<xref:System.Data.DataRowVersion.Current>) 版本。 例如, 在调用`AcceptChanges`方法之前, 应用程序可以访问记录的不同版本 (在<xref:System.Data.DataRowVersion>枚举中定义), 并相应地处理所做的更改。

> [!NOTE]
> 行的不同版本仅在已编辑或在调用`AcceptChanges`方法之前存在。 `AcceptChanges`调用方法后, 当前版本和原始版本是相同的。

将<xref:System.Data.DataRowVersion>值与列索引 (或字符串形式的列名称) 一起传递将从该列的特定行版本返回值。 在<xref:System.Data.DataTable.ColumnChanging> 和<xref:System.Data.DataTable.ColumnChanged>事件期间, 会标识已更改的列。 这是检查不同行版本以进行验证的好时机。 但是, 如果您暂时挂起了约束, 则不会引发这些事件, 您将需要以编程方式标识哪些列已更改。 为此, 可以循环访问<xref:System.Data.DataTable.Columns%2A>集合并比较不同<xref:System.Data.DataRowVersion>的值。

### <a name="to-get-the-original-version-of-a-record"></a>获取记录的原始版本

- 通过传入<xref:System.Data.DataRowVersion>要返回的行的来访问该列的值。

     下面的示例演示如何使用<xref:System.Data.DataRowVersion>值获取中<xref:System.Data.DataRow>的`CompanyName`字段的原始值:

     [!code-csharp[VbRaddataEditing#21](../data-tools/codesnippet/CSharp/validate-data-in-datasets_6.cs)]
     [!code-vb[VbRaddataEditing#21](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_6.vb)]

## <a name="access-the-current-version-of-a-datarow"></a>访问 DataRow 的当前版本

### <a name="to-get-the-current-version-of-a-record"></a>获取记录的当前版本

- 访问列的值, 然后向该索引添加一个参数, 用于指示要返回的行的版本。

     下面的示例演示如何使用<xref:System.Data.DataRowVersion>值获取中<xref:System.Data.DataRow>的`CompanyName`字段的当前值:

     [!code-csharp[VbRaddataEditing#22](../data-tools/codesnippet/CSharp/validate-data-in-datasets_7.cs)]
     [!code-vb[VbRaddataEditing#22](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_7.vb)]

## <a name="see-also"></a>请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [如何：验证 Windows 窗体 DataGridView 控件中的数据](/dotnet/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control)
- [如何：显示用于通过 Windows 窗体 ErrorProvider 组件进行的窗体验证的错误图标](/dotnet/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider)