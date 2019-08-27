---
title: 验证数据集中 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2a6993d241f49261131ffad76dc50534ac8e1591
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694881"
---
# <a name="validate-data-in-datasets"></a>验证数据集中的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

验证数据是输入到数据对象的值符合数据集的架构内的约束的确认过程。 验证过程还确认这些值都遵循已为你的应用程序建立的规则。 最好验证之前将更新发送到基础数据库的数据。 这将减少错误，以及潜在的应用程序和数据库之间的往返行程量。  
  
 你可以确认正在写入到数据集的数据是通过构建到数据集本身的验证检查有效。 数据集可以检查的数据，无论执行更新时正在 — 不管是直接通过控件在表单中，在一个组件，或以其他方式。 因为数据集 （不同于数据库后端） 应用程序的一部分，它是生成特定于应用程序的验证逻辑位置。  
  
 将验证添加到你的应用程序的最佳位置是在数据集的分部类文件中。 在中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]或[!INCLUDE[csprcs](../includes/csprcs-md.md)]，打开**数据集设计器**，然后双击你想要创建验证的列或表。 此操作将自动创建<xref:System.Data.DataTable.ColumnChanging>或<xref:System.Data.DataTable.RowChanging>事件处理程序。 有关详细信息，请参阅[如何：在列更改过程中验证数据](https://msdn.microsoft.com/library/a2680600-67b6-4a40-a77e-b5bc638281c5)或[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。 有关完整示例，请参阅[演练：向数据集添加验证](https://msdn.microsoft.com/library/09351fab-d670-45e3-b53a-a944eff717e7)。  
  
## <a name="validate-data"></a>验证数据  
 在数据集中的验证可以通过以下方式完成：  
  
- 通过创建自己的特定于应用程序的验证，可在更改过程中检查各个数据列中的值。  有关详细信息，请参阅[如何：在列更改过程中验证数据](https://msdn.microsoft.com/library/a2680600-67b6-4a40-a77e-b5bc638281c5)。  
  
- 通过创建自己的特定于应用程序的验证，可以检查整个数据时对值的数据行发生了变化。 有关详细信息，请参阅[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。  
  
- 通过创建关键字、 唯一约束，等等为数据集的实际架构定义的一部分。 有关将验证合并到的架构定义的详细信息，请参阅[限制为包含唯一值 DataColumn](https://msdn.microsoft.com/library/8ca21f77-b99a-47a7-a656-7cfd7a1bd9df)。  
  
- 通过设置的属性<xref:System.Data.DataColumn>对象，如<xref:System.Data.DataColumn.MaxLength%2A>， <xref:System.Data.DataColumn.AllowDBNull%2A>，和<xref:System.Data.DataColumn.Unique%2A>。  
  
  多个事件引发的<xref:System.Data.DataTable>对象记录中发生更改时：  
  
- <xref:System.Data.DataTable.ColumnChanging>和<xref:System.Data.DataTable.ColumnChanged>期间和之后的单个列对每个更改，则会引发事件。 <xref:System.Data.DataTable.ColumnChanging>事件非常有用，当你想要验证的特定列中的更改。 有关建议的更改的信息作为与事件自变量传递。 有关详细信息，请参阅[如何：在列更改过程中验证数据](https://msdn.microsoft.com/library/a2680600-67b6-4a40-a77e-b5bc638281c5)。  
  
- <xref:System.Data.DataTable.RowChanging>和<xref:System.Data.DataTable.RowChanged>引发事件期间和之后任何行中的更改。 <xref:System.Data.DataTable.RowChanging>事件是更多常规。 它表示在一行中，某个位置发生更改，但不知道哪些列发生改变。 有关详细信息，请参阅[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。  
  
  默认情况下，对列的每个更改因此引发四个事件。 第一个是<xref:System.Data.DataTable.ColumnChanging>和<xref:System.Data.DataTable.ColumnChanged>正在更改的特定列的事件。 接下来是<xref:System.Data.DataTable.RowChanging>和<xref:System.Data.DataTable.RowChanged>事件。 如果对行进行了多个更改，每次更改都会引发事件。  
  
> [!NOTE]
> 数据行<xref:System.Data.DataRow.BeginEdit%2A>方法会关闭<xref:System.Data.DataTable.RowChanging>和<xref:System.Data.DataTable.RowChanged>后每个单独的列更改事件。 在这种情况下，不会引发事件之前<xref:System.Data.DataRow.EndEdit%2A>已调用方法，当<xref:System.Data.DataTable.RowChanging>和<xref:System.Data.DataTable.RowChanged>只需一次引发事件。 有关详细信息，请参阅[填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。  
  
 您选择的事件取决于想要验证的粒度级别。 如果必须立即列发生更改时捕获错误，通过使用构建验证<xref:System.Data.DataTable.ColumnChanging>事件。 否则，请使用<xref:System.Data.DataTable.RowChanging>事件，这可能会导致同时捕获多个错误。 此外，如果你的数据结构化的因此基于另一列的内容验证某一列的值，则执行过程中的验证<xref:System.Data.DataTable.RowChanging>事件。  
  
 当更新记录时，<xref:System.Data.DataTable>对象引发并更改发生更改后可以响应的事件。  
  
 如果应用程序使用类型化数据集，则可以创建强类型化的事件处理程序。 这将添加四个可以创建处理程序的其他类型化的事件： `dataTableNameRowChanging`， `dataTableNameRowChanged`， `dataTableNameRowDeleting`，和`dataTableNameRowDeleted`。 这些类型化的事件处理程序传递参数，包括使代码更易于读取和写入您的表的列名称。  
  
## <a name="data-update-events"></a>数据更新事件  
  
|Event|描述|  
|-----------|-----------------|  
|<xref:System.Data.DataTable.ColumnChanging>|正在更改的列中值。 该事件，传递的行和列以及建议的新值。|  
|<xref:System.Data.DataTable.ColumnChanged>|列中的值已更改。 该事件，传递的行和列以及建议的值。|  
|<xref:System.Data.DataTable.RowChanging>|对所做的更改<xref:System.Data.DataRow>对象即将被提交到数据集返回。 如果您不调用<xref:System.Data.DataRow.BeginEdit%2A>方法，<xref:System.Data.DataTable.RowChanging>个列对每个更改都会引发事件后立即<xref:System.Data.DataTable.ColumnChanging>引发事件。 如果您调用<xref:System.Data.DataRow.BeginEdit%2A>进行更改之前,<xref:System.Data.DataTable.RowChanging>仅当您调用时引发事件<xref:System.Data.DataRow.EndEdit%2A>方法。<br /><br /> 该事件传递的行，以及一个值，该值指示所执行操作 （如更改、 插入、 等） 的类型。|  
|<xref:System.Data.DataTable.RowChanged>|已更改行。 该事件传递的行，以及一个值，该值指示所执行操作 （如更改、 插入、 等） 的类型。|  
|<xref:System.Data.DataTable.RowDeleting>|删除了某行。 该事件传递的行，以及一个值，该值指示所执行操作 （删除） 的类型。|  
|<xref:System.Data.DataTable.RowDeleted>|行已被删除。 该事件传递的行，以及一个值，该值指示所执行操作 （删除） 的类型。|  
  
 <xref:System.Data.DataTable.ColumnChanging>， <xref:System.Data.DataTable.RowChanging>，和<xref:System.Data.DataTable.RowDeleting>更新过程中引发事件。 这些事件可用于验证数据或执行其他类型的处理。 由于在这些事件中，更新正在进行，您可以取消它通过引发异常，这会阻止从更新完成。  
  
 <xref:System.Data.DataTable.ColumnChanged>，<xref:System.Data.DataTable.RowChanged>和<xref:System.Data.DataTable.RowDeleted>事件是更新已成功完成时引发的通知事件。 当你想要采取进一步的措施根据成功更新时，这些事件非常有用。  
  
## <a name="validate-data-during-column-changes"></a>在列更改过程中验证数据  
  
> [!NOTE]
> **数据集设计器**创建一个分部类，可以在哪些验证逻辑添加到数据集。 设计器生成数据集不会删除或更改的分部类中的任何代码。  
  
 通过响应中的数据列的值更改时，可以验证数据<xref:System.Data.DataTable.ColumnChanging>事件。 当引发，此事件将传递的事件自变量 (<xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A>)，其中包含个当前列的建议的值。 基于内容的`e.ProposedValue`，你可以：  
  
- 接受建议的值，方法不执行任何操作。  
  
- 通过设置列错误拒绝建议的值 (<xref:System.Data.DataRow.SetColumnError%2A>) 从列更改事件处理程序中。  
  
- （可选） 使用<xref:System.Windows.Forms.ErrorProvider>控件来向用户显示一条错误消息。 有关详细信息，请参阅[ErrorProvider 组件](https://msdn.microsoft.com/library/c0f2e231-c5c9-413d-a507-75af2db499b6)。  
  
  此外可以在执行验证<xref:System.Data.DataTable.RowChanging>事件。 有关详细信息，请参阅[如何：在行更改过程中验证数据](https://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)。  
  
## <a name="validate-data-during-row-changes"></a>在行更改过程中验证数据  
 可以编写代码以验证你想要验证每个的列包含满足要求的应用程序的数据。 为此，设置该列以指示其包含一个错误，是否建议的值是不可接受。 下面的示例设置列错误时`Quantity`列是小于或等于 0。 行更改事件处理程序应类似于下面的示例。  
  
#### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>若要验证数据的行时将更改 (Visual Basic)  
  
1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。  
  
2. 双击想要验证的表的标题栏。 此操作将自动创建<xref:System.Data.DataTable.RowChanging>事件处理程序<xref:System.Data.DataTable>数据集的分部类文件中。  
  
    > [!TIP]
    > 双击要创建的行更改的事件处理程序的表名称的左侧。 如果您双击表名，可以对其进行编辑。  
  
     [!code-vb[VbRaddataValidating#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataValidating/VB/NorthwindDataSet.vb#3)]  
  
#### <a name="to-validate-data-when-a-row-changes-c"></a>若要验证数据的行时更改 (C#)  
  
1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。  
  
2. 双击想要验证的表的标题栏。 此操作将创建的分部类文件<xref:System.Data.DataTable>。  
  
    > [!NOTE]
    > **数据集设计器**不会自动创建的事件处理程序<xref:System.Data.DataTable.RowChanging>事件。 您必须创建一个方法来处理<xref:System.Data.DataTable.RowChanging>挂接表的初始化方法中的事件的事件，并运行的代码。  
  
3. 将以下代码复制到分部类：  
  
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
  
## <a name="to-retrieve-changed-rows"></a>若要检索已更改的行  
 数据表中的每一行都具有<xref:System.Data.DataRow.RowState%2A>跟踪使用中的值的行的当前状态的属性<xref:System.Data.DataRowState>枚举。 可以从数据集或数据的表中返回已更改的行通过调用`GetChanges`方法<xref:System.Data.DataSet>或<xref:System.Data.DataTable>。 你可以验证更改存在之前调用`GetChanges`通过调用<xref:System.Data.DataSet.HasChanges%2A>数据集的方法。 有关 <xref:System.Data.DataSet.HasChanges%2A> 的详细信息，请参阅[如何：检查是否已更改的行](https://msdn.microsoft.com/library/af160d20-472b-4c13-8f15-75480c39a653)。  
  
> [!NOTE]
> 将更改提交到数据集或数据的表后 (通过调用<xref:System.Data.DataSet.AcceptChanges%2A>方法)，则`GetChanges`方法不返回任何数据。 如果你的应用程序需要处理已更改的行，必须处理的更改之前，调用`AcceptChanges`方法。  
  
 调用<xref:System.Data.DataSet.GetChanges%2A>数据集或数据的表的方法将返回包含已更改的唯一记录的新数据集或数据表。 如果你想要获取特定的记录 — 例如，只是新记录或已修改的记录 — 可以将传递的值<xref:System.Data.DataRowState>枚举作为参数`GetChanges`方法。  
  
 使用<xref:System.Data.DataRowVersion>枚举要访问的行 （例如，在处理它之前的行中的原始值） 的不同版本。  
  
#### <a name="to-get-all-changed-records-from-a-dataset"></a>若要获取所有已更改的记录来自数据集  
  
- 调用<xref:System.Data.DataSet.GetChanges%2A>数据集的方法。  
  
     下面的示例创建名为的新数据集`changedRecords`并填充名为的另一数据集的所有更改记录`dataSet1`。  
  
     [!code-csharp[VbRaddataEditing#14](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#14)]
     [!code-vb[VbRaddataEditing#14](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#14)]  
  
#### <a name="to-get-all-changed-records-from-a-data-table"></a>若要获取所有已更改的记录从数据表  
  
- 调用<xref:System.Data.DataTable.GetChanges%2A>的数据表的方法。  
  
     下面的示例创建名为的新数据表`changedRecordsTable`并填充名为的另一个数据表中的所有更改记录`dataTable1`。  
  
     [!code-csharp[VbRaddataEditing#15](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#15)]
     [!code-vb[VbRaddataEditing#15](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#15)]  
  
#### <a name="to-get-all-records-that-have-a-specific-row-state"></a>若要获取的特定行状态的所有记录  
  
- 调用`GetChanges`方法的数据集或数据表并传递<xref:System.Data.DataRowState>枚举值作为参数。  
  
     下面的示例演示如何创建名为的新数据集`addedRecords`并仅填充已添加到的记录`dataSet1`数据集。  
  
     [!code-csharp[VbRaddataEditing#16](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#16)]
     [!code-vb[VbRaddataEditing#16](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#16)]  
  
- 下面的示例演示如何返回最近添加到的所有记录`Customers`表：  
  
     [!code-csharp[VbRaddataEditing#17](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#17)]
     [!code-vb[VbRaddataEditing#17](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#17)]  
  
## <a name="access-the-original-version-of-a-datarow"></a>访问 DataRow 的原始版本  
 数据集时对数据行进行了更改，将保留原始 (<xref:System.Data.DataRowVersion>) 和新 (<xref:System.Data.DataRowVersion>) 行的版本。 例如，之前调用`AcceptChanges`方法，你的应用程序可以访问一条记录的不同版本 (如中所定义<xref:System.Data.DataRowVersion>枚举) 并相应地处理所做的更改。  
  
> [!NOTE]
> 行的不同版本存在仅已经过编辑之后，并在它`AcceptChanges`调用方法。 之后`AcceptChanges`调用方法、 当前和原始版本都相同。  
  
 传递<xref:System.Data.DataRowVersion>值的列索引 （或字符串形式的列名称） 以及返回该列的特定行版本中的值。 期间标识已更改的列<xref:System.Data.DataTable.ColumnChanging>和<xref:System.Data.DataTable.ColumnChanged>事件。 这是检查出于验证目的的不同行版本的好时机。 但是，如果暂时挂起了约束，不会引发这些事件，并且将需要以编程方式确定哪些列发生了更改。 您可以执行此操作，可以循环访问<xref:System.Data.DataTable.Columns%2A>集合并比较不同<xref:System.Data.DataRowVersion>值。  
  
#### <a name="to-get-the-original-version-of-a-record"></a>若要获取一条记录的原始版本  
  
- 通过传入访问列的值<xref:System.Data.DataRowVersion>你想要返回的行。  
  
     下面的示例演示如何使用<xref:System.Data.DataRowVersion>若要获取的原始值的值`CompanyName`字段中<xref:System.Data.DataRow>:  
  
     [!code-csharp[VbRaddataEditing#21](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#21)]
     [!code-vb[VbRaddataEditing#21](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#21)]  
  
## <a name="access-the-current-version-of-a-datarow"></a>访问数据行的当前版本  
  
#### <a name="to-get-the-current-version-of-a-record"></a>若要获取一条记录的当前版本  
  
- 访问的列的值，然后将参数添加到索引，指示你想要返回的行版本。  
  
     下面的示例演示如何使用<xref:System.Data.DataRowVersion>要获取的当前值的值`CompanyName`字段中<xref:System.Data.DataRow>:  
  
     [!code-csharp[VbRaddataEditing#22](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#22)]
     [!code-vb[VbRaddataEditing#22](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#22)]  
  
## <a name="see-also"></a>请参阅

- [如何：验证 Windows 窗体 DataGridView 控件中的数据](https://msdn.microsoft.com/library/d10aef35-701e-4a3c-a684-2a2ed1aeaca6)   
- [如何：对于表格验证使用 Windows 窗体 ErrorProvider 组件显示错误图标](https://msdn.microsoft.com/library/3b681a32-9db4-497b-a34b-34980eabee46)