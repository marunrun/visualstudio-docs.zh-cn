---
title: 将数据保存回数据库
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- datasets [Visual Basic], validating data
- data validation, datasets
- data [Visual Studio], saving
- row version
- updating datasets, constraints
- datasets [Visual Basic], about datasets
- datasets [Visual Basic], merging
- updates, constraints in datasets
- saving data, about saving data
- datasets [Visual Basic], constraints
- TableAdapters
ms.assetid: afe6cb8a-dc6a-428b-b07b-903ac02c890b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 493637f81df15fadf65d6c7d90e980e322919b13
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281742"
---
# <a name="save-data-back-to-the-database"></a>将数据保存回数据库

数据集是数据的内存中副本。 如果修改这些数据，最好将这些更改保存回数据库。 可以通过以下三种方式之一执行此操作：

- 通过调用 `Update` TableAdapter 的方法之一

- 通过调用 TableAdapter 的 `DBDirect` 方法之一

- `UpdateAll`当数据集包含与 dataset 中的其他表相关的表时，通过在 Visual Studio 为您生成的 TableAdapterManager 上调用方法

将数据集表数据绑定到 Windows 窗体或 XAML 页上的控件时，数据绑定体系结构将完成所有工作。

如果熟悉 Tableadapter，可以直接跳转到以下主题之一：

|主题|说明|
|-----------|-----------------|
|[将新记录插入数据库](../data-tools/insert-new-records-into-a-database.md)|如何使用 Tableadapter 或 Command 对象执行更新和插入操作|
|[使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)|如何通过 Tableadapter 执行更新|
|[分层更新](../data-tools/hierarchical-update.md)|如何从包含两个或多个相关表的数据集执行更新|
|[处理并发异常](../data-tools/handle-a-concurrency-exception.md)|如果两个用户尝试同时更改数据库中的相同数据，如何处理异常|
|[如何：通过使用事务来保存数据](../data-tools/save-data-by-using-a-transaction.md)|如何使用系统在事务中保存数据。 事务命名空间和 TransactionScope 对象|
|[在事务中保存数据](../data-tools/save-data-in-a-transaction.md)|创建 Windows 窗体应用程序的演练，用于演示如何将数据保存到事务中的数据库|
|[将数据保存到数据库（多个表）](../data-tools/save-data-to-a-database-multiple-tables.md)|如何编辑记录并将多个表中的更改保存回数据库|
|[将数据从对象保存到数据库](../data-tools/save-data-from-an-object-to-a-database.md)|如何使用 TableAdapter DbDirect 方法将数据从数据集中的对象传递到数据库|
|[用 TableAdapter DBDirect 方法保存数据](../data-tools/save-data-with-the-tableadapter-dbdirect-methods.md)|如何使用 TableAdapter 将 SQL 查询直接发送到数据库|
|[将数据集另存为 XML](../data-tools/save-a-dataset-as-xml.md)|如何将数据集保存到 XML 文档|

## <a name="two-stage-updates"></a>两阶段更新

更新数据源的过程分为两个步骤。 第一步是更新包含新记录、已更改记录或已删除记录的数据集。 如果应用程序永远不会将这些更改发送回数据源，则已完成更新。

如果将更改发送回数据库，则需要执行第二步。 如果未使用数据绑定控件，则必须手动调用 `Update` 用于填充数据集的同一 TableAdapter （或数据适配器）的方法。 不过，您也可以使用不同的适配器，例如，将数据从一个数据源移动到另一个数据源，或更新多个数据源。 如果不使用数据绑定，并且要保存对相关表所做的更改，则必须手动实例化自动生成的类的变量 `TableAdapterManager` ，然后调用其 `UpdateAll` 方法。

![数据集更新的概念图](../data-tools/media/vbdatasetupdates.gif)

数据集包含表的集合，其中包含行的集合。 如果要在以后更新基础数据源，则必须在 `DataTable.DataRowCollection` 添加或删除行时对属性使用方法。 这些方法执行更新数据源所需的更改跟踪。 如果对 `RemoveAt` Rows 属性调用集合，则不会将删除操作返回到数据库。

## <a name="merge-datasets"></a>合并数据集

可以通过将数据集与其他数据集*合并*来更新该数据集的内容。 这涉及到将*源*数据集的内容复制到调用数据集（称为*目标*数据集）。 合并数据集时，源数据集中的新记录将添加到目标数据集。 此外，还会将源数据集中的额外列添加到目标数据集。 如果你有本地数据集，并且从另一个应用程序获得另一个数据集，则合并数据集会很有用。 当你从组件（例如 XML web services）获取第二个数据集时，或者当你需要集成多个数据集的数据时，这也很有用。

合并数据集时，可以传递布尔参数（ `preserveChanges` ），该参数告知 <xref:System.Data.DataSet.Merge%2A> 方法是否保留目标数据集中的现有修改。 由于数据集维护多个版本的记录，因此请务必记住多个版本的记录正在合并。 下表显示了如何合并两个数据集中的记录：

|DataRowVersion|目标数据集|源数据集|
| - | - | - |
|原始|James Wilson|James C. Wilson|
|当前|Jim Wilson|James C. Wilson|

<xref:System.Data.DataSet.Merge%2A>对上表调用方法会 `preserveChanges=false targetDataset.Merge(sourceDataset)` 生成以下数据：

|DataRowVersion|目标数据集|源数据集|
| - | - | - |
|原始|James C. Wilson|James C. Wilson|
|当前|James C. Wilson|James C. Wilson|

如果调用 <xref:System.Data.DataSet.Merge%2A> 方法， `preserveChanges = true targetDataset.Merge(sourceDataset, true)` 将生成以下数据：

|DataRowVersion|目标数据集|源数据集|
| - | - | - |
|原始|James C. Wilson|James C. Wilson|
|当前|Jim Wilson|James C. Wilson|

> [!CAUTION]
> 在此 `preserveChanges = true` 方案中，如果对 <xref:System.Data.DataSet.RejectChanges%2A> 目标数据集中的记录调用了方法，则它将恢复为*源*数据集中的原始数据。 这意味着，如果尝试用目标数据集更新原始数据源，则它可能无法找到要更新的原始行。 您可以通过使用数据源中已更新的记录填充另一个数据集，然后执行合并来防止发生并发冲突，从而防止并发冲突。 （当其他用户在填充数据集后修改数据源中的记录时，将发生并发冲突。）

## <a name="update-constraints"></a>更新约束

若要对现有数据行进行更改，请在单独的列中添加或更新数据。 如果数据集包含约束（例如，外键或不可为 null 的约束），则在您更新记录时，可能会暂时处于错误状态。 也就是说，在您完成更新一列后，但在到达下一个列之前，它可能处于错误状态。

若要防止过早的约束冲突，可以暂时挂起更新约束。 这有两种用途：

- 它可防止在完成更新一列但尚未开始更新其他列后引发错误。

- 它禁止引发某些更新事件（通常用于验证的事件）。

> [!NOTE]
> 在 Windows 窗体中，datagrid 中内置的数据绑定体系结构会挂起约束检查，直到焦点移出行为止，并且无需显式调用 <xref:System.Data.DataRow.BeginEdit%2A> 、 <xref:System.Data.DataRow.EndEdit%2A> 或 <xref:System.Data.DataRow.CancelEdit%2A> 方法。

当在 <xref:System.Data.DataSet.Merge%2A> 数据集上调用方法时，将自动禁用约束。 合并完成后，如果不能启用对数据集的任何约束， <xref:System.Data.ConstraintException> 则会引发。 在这种情况下， <xref:System.Data.DataSet.EnforceConstraints%2A> 属性设置为，并且在将 `false,` 属性重置为之前，必须解决所有约束冲突 <xref:System.Data.DataSet.EnforceConstraints%2A> `true` 。

完成更新后，你可以重新启用约束检查，这也会重新启用更新事件并引发它们。

有关挂起事件的详细信息，请参阅[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

## <a name="dataset-update-errors"></a>数据集更新错误

更新数据集中的记录时，可能会出现错误。 例如，您可能无意中将错误类型的数据写入列、过长的数据或具有其他一些完整性问题的数据。 或者，你可能具有特定于应用程序的验证检查，这些检查可能在更新事件的任何阶段引发自定义错误。 有关详细信息，请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)。

## <a name="maintain-information-about-changes"></a>维护有关更改的信息

有关数据集中的更改的信息可通过两种方式进行维护：标记指示它们已更改的行（ <xref:System.Data.DataRow.RowState%2A> ），以及保留记录的多个副本（ <xref:System.Data.DataRowVersion> ）。 通过使用此信息，进程可以确定数据集中发生了哪些更改，并可以将适当的更新发送到数据源。

### <a name="rowstate-property"></a>RowState 属性

<xref:System.Data.DataRow.RowState%2A>对象的属性 <xref:System.Data.DataRow> 是一个值，它提供有关特定数据行的状态的信息。

下表详细说明了枚举的可能值 <xref:System.Data.DataRowState> ：

|DataRowState 值|说明|
| - |-----------------|
|<xref:System.Data.DataRowState.Added>|该行已作为项添加到 <xref:System.Data.DataRowCollection> 中。 （此状态中的行没有相应的原始版本，因为在调用最后一个方法时它不存在 <xref:System.Data.DataRow.AcceptChanges%2A> ）。|
|<xref:System.Data.DataRowState.Deleted>|已使用对象的删除行 <xref:System.Data.DataRow.Delete%2A> <xref:System.Data.DataRow> 。|
|<xref:System.Data.DataRowState.Detached>|已创建该行，但它不是任何 <xref:System.Data.DataRowCollection> 的一部分。 <xref:System.Data.DataRow>对象在创建后立即处于此状态，在将其添加到集合之前，以及在将其从集合中删除之后。|
|<xref:System.Data.DataRowState.Modified>|行中的列值在某种程度上已更改。|
|<xref:System.Data.DataRowState.Unchanged>|自上一次调用 <xref:System.Data.DataRow.AcceptChanges%2A> 之后，该行未更改。|

### <a name="datarowversion-enumeration"></a>DataRowVersion 枚举

数据集维护记录的多个版本。 <xref:System.Data.DataRowVersion> <xref:System.Data.DataRow> 使用 <xref:System.Data.DataRow.Item%2A> 对象的属性或方法检索在中找到的值时，将使用这些字段 <xref:System.Data.DataRow.GetChildRows%2A> <xref:System.Data.DataRow> 。

下表详细说明了枚举的可能值 <xref:System.Data.DataRowVersion> ：

|DataRowVersion 值|说明|
| - |-----------------|
|<xref:System.Data.DataRowVersion.Current>|记录的当前版本包含自上次调用以来对记录执行的所有修改 <xref:System.Data.DataRow.AcceptChanges%2A> 。 如果已删除行，则没有当前版本。|
|<xref:System.Data.DataRowVersion.Default>|数据集架构或数据源定义的记录的默认值。|
|<xref:System.Data.DataRowVersion.Original>|记录的原始版本是记录的副本，这与上次在数据集中提交更改的时间相同。 在实际情况下，这通常是从数据源读取的记录的版本。|
|<xref:System.Data.DataRowVersion.Proposed>|所建议的记录版本，该记录在你处于更新期间（即，调用方法和方法时）暂时可用 <xref:System.Data.DataRow.BeginEdit%2A> <xref:System.Data.DataRow.EndEdit%2A> 。 通常，可以在事件（如）的处理程序中访问记录的建议版本 <xref:System.Data.DataTable.RowChanging> 。 调用 <xref:System.Data.DataRow.CancelEdit%2A> 方法会反转更改，并删除建议的数据行版本。|

将更新信息传输到数据源时，原始版本和当前版本非常有用。 通常，将更新发送到数据源时，数据库的新信息将位于记录的当前版本中。 原始版本中的信息用于查找要更新的记录。

例如，在记录的主键发生更改的情况下，您需要一种方法，以便在数据源中查找正确的记录以更新更改。 如果不存在原始版本，则记录很可能会追加到数据源中，这不仅会导致额外的不需要记录，还会导致一条不准确和过时的记录。 并发控制中也使用了这两个版本。 您可以将原始版本与数据源中的记录进行比较，以确定记录是否在加载到数据集后发生了更改。

如果需要在实际将更改提交到数据集之前执行验证，则建议的版本非常有用。

即使记录已更改，也没有该行的原始或当前版本。 将新行插入到表中时，没有原始版本，只有当前版本。 同样，如果您通过调用表的方法来删除行 `Delete` ，则有原始版本，但没有当前版本。

您可以通过查询数据行的方法来测试是否存在特定的记录版本 <xref:System.Data.DataRow.HasVersion%2A> 。 在 <xref:System.Data.DataRowVersion> 请求列的值时，可以通过将枚举值作为可选参数传递来访问记录的任一版本。

## <a name="get-changed-records"></a>获取已更改的记录

这是一种常见的做法是不更新数据集中的每个记录。 例如，用户可能正在使用 <xref:System.Windows.Forms.DataGridView> 显示多个记录的 Windows 窗体控件。 但是，用户可能只更新几条记录，删除一个记录，然后插入一个新记录。 数据集和数据表提供了一个方法（ `GetChanges` ），用于仅返回已修改的行。

您可以使用数据表 `GetChanges` （ <xref:System.Data.DataTable.GetChanges%2A> ）或数据集（）本身的方法创建已更改记录的子集 <xref:System.Data.DataSet.GetChanges%2A> 。 如果调用数据表的方法，它将返回仅包含已更改记录的表的副本。 同样，如果在数据集上调用方法，则会获得一个新的数据集，其中仅包含已更改的记录。

`GetChanges`本身返回所有已更改的记录。 与此相反，通过将所需的 <xref:System.Data.DataRowState> 作为参数传递给 `GetChanges` 方法，可以指定所需的已更改记录子集：新添加的记录、标记为删除的记录、已分离的记录或已修改的记录。

当您想要将记录发送给另一个组件进行处理时，获取已更改记录的子集很有用。 您可以通过仅获取组件所需的记录来减少与其他组件通信的开销，而不是发送整个数据集。

## <a name="commit-changes-in-the-dataset"></a>提交数据集中的更改

在数据集中进行更改时， <xref:System.Data.DataRow.RowState%2A> 将设置已更改行的属性。 记录的原始版本和当前版本将通过属性建立、维护和提供 <xref:System.Data.DataRowView.RowVersion%2A> 。 在这些已更改行的属性中存储的元数据是将正确的更新发送到数据源所必需的。

如果更改反映了数据源的当前状态，则不再需要保留此信息。 通常，当数据集与其源同步时，有两次：

- 将信息加载到数据集之后（例如从数据源读取数据时）。

- 在将数据集的更改发送到数据源之后（但不是在之前），因为您将丢失将更改发送到数据库所需的更改信息。

可以通过调用方法将挂起的更改提交到数据集 <xref:System.Data.DataSet.AcceptChanges%2A> 。 通常， <xref:System.Data.DataSet.AcceptChanges%2A> 在下列时间调用：

- 加载数据集之后。 如果通过调用 TableAdapter 的方法加载数据集 `Fill` ，则适配器会自动为你提交更改。 但是，如果通过将其他数据集合并到数据集来加载数据集，则必须手动提交这些更改。

    > [!NOTE]
    > 您可以 `Fill` 通过将 `AcceptChangesDuringFill` 适配器的属性设置为来阻止适配器在调用方法时自动提交更改 `false` 。 如果将其设置为 `false` ，则在 <xref:System.Data.DataRow.RowState%2A> 填充过程中插入的每一行的均设置为 <xref:System.Data.DataRowState.Added> 。

- 将数据集更改发送到另一个进程（如 XML web services）之后。

    > [!CAUTION]
    > 以这种方式提交更改会删除任何更改信息。 在完成执行要求应用程序了解在数据集中所做的更改的操作之前，不要提交更改。

此方法完成以下操作：

- <xref:System.Data.DataRowVersion.Current>将记录版本写入其 <xref:System.Data.DataRowVersion.Original> 版本，并覆盖原始版本。

- 删除 <xref:System.Data.DataRow.RowState%2A> 属性设置为的任何行 <xref:System.Data.DataRowState.Deleted> 。

- 将 <xref:System.Data.DataRow.RowState%2A> 记录的属性设置为 <xref:System.Data.DataRowState.Unchanged> 。

<xref:System.Data.DataSet.AcceptChanges%2A>方法在三个级别提供。 您可以对对象调用此方法 <xref:System.Data.DataRow> ，以便只为该行提交更改。 您还可以对对象调用它 <xref:System.Data.DataTable> 以提交表中的所有行。 最后，您可以对对象调用它 <xref:System.Data.DataSet> 以提交数据集的所有表的所有记录中的所有挂起的更改。

下表说明了根据调用方法的对象提交的更改：

|方法|结果|
|------------|------------|
|<xref:System.Data.DataRow.AcceptChanges%2A?displayProperty=fullName>|仅在特定行上提交更改。|
|<xref:System.Data.DataTable.AcceptChanges%2A?displayProperty=fullName>|对特定表中的所有行提交更改。|
|<xref:System.Data.DataSet.AcceptChanges%2A?displayProperty=fullName>|在数据集的所有表中的所有行上提交更改。|

> [!NOTE]
> 如果通过调用 TableAdapter 的方法加载数据集 `Fill` ，则无需显式接受更改。 默认情况下， `Fill` 方法在 `AcceptChanges` 完成数据表填充后调用方法。

相关方法会 <xref:System.Data.DataSet.RejectChanges%2A> 通过将 <xref:System.Data.DataRowVersion.Original> 版本复制回记录版本来撤消更改的效果 <xref:System.Data.DataRowVersion.Current> 。 它还将 <xref:System.Data.DataRow.RowState%2A> 每个记录的设置回 <xref:System.Data.DataRowState.Unchanged> 。

## <a name="data-validation"></a>数据验证

为了验证应用程序中的数据是否满足其传递到的进程的要求，您通常必须添加验证。 这可能涉及到检查窗体中的用户输入是否正确、验证其他应用程序发送给应用程序的数据，甚至检查在组件中计算的信息是否在数据源和应用程序要求的约束范围内。

可以通过多种方式验证数据：

- 在业务层中，通过将代码添加到应用程序来验证数据。 数据集是您可以执行此操作的一个位置。 数据集提供后端验证的一些优点，例如，能够在更改列和行值时验证更改。 有关详细信息，请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)。

- 在表示层中，通过向窗体添加验证。 有关详细信息，请参阅[Windows 窗体中的用户输入验证](/dotnet/framework/winforms/user-input-validation-in-windows-forms)。

- 在数据后端，将数据发送到数据源（例如数据库），并允许数据源接受或拒绝数据。 如果您使用的数据库具有用于验证数据和提供错误信息的复杂设施，则这可能是一种可行的方法，因为无论数据来自何处，都可以验证数据。 但是，这种方法可能无法满足特定于应用程序的验证要求。 此外，使数据源验证数据可能会导致大量与数据源的往返，具体取决于应用程序如何帮助解决后端引发的验证错误。

   > [!IMPORTANT]
   > 将数据命令与设置为的属性结合使用时，请在将 <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> <xref:System.Data.CommandType.Text> 客户端传递到数据库之前，仔细检查从该客户端发送的信息。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 将用户输入传输到数据库之前，请始终验证信息是否有效。 最佳做法是尽可能使用参数化查询或存储过程。

## <a name="transmit-updates-to-the-data-source"></a>将更新传输到数据源

在数据集中进行更改后，您可以将这些更改传输到数据源。 最常见的是通过调用 `Update` TableAdapter （或数据适配器）的方法来执行此操作。 方法遍历数据表中的每个记录，确定需要哪种类型的更新（更新、插入或删除）（如果有），然后运行适当的命令。

为了说明如何进行更新，假设你的应用程序使用包含单个数据表的数据集。 应用程序从数据库中提取两行。 检索完成后，内存中数据表的外观如下所示：

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Unchanged)    c400         Nancy Buchanan    Pending
```

应用程序将林丹的状态更改为 "首选"。 由于此更改，该行的属性的值 <xref:System.Data.DataRow.RowState%2A> 从更改 <xref:System.Data.DataRowState.Unchanged> 为 <xref:System.Data.DataRowState.Modified> 。 第一行的属性的值将 <xref:System.Data.DataRow.RowState%2A> 保持不变 <xref:System.Data.DataRowState.Unchanged> 。 数据表现在如下所示：

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Modified)     c400         Nancy Buchanan    Preferred
```

应用程序现在调用 `Update` 方法，将数据集传送给数据库。 方法依次检查每一行。 对于第一行，该方法不会将 SQL 语句传输到数据库，因为该行自最初从数据库提取以来未发生更改。

但对于第二行， `Update` 方法会自动调用正确的数据命令并将其传输到数据库。 SQL 语句的特定语法取决于基础数据存储所支持的 SQL 的方言。 但以下是已传输的 SQL 语句的一般特征：

- 传输的 SQL 语句是 UPDATE 语句。 适配器知道要使用 UPDATE 语句，因为属性的值 <xref:System.Data.DataRow.RowState%2A> 为 <xref:System.Data.DataRowState.Modified> 。

- 传输的 SQL 语句包含一个 WHERE 子句，该子句指示 UPDATE 语句的目标为行 `CustomerID = 'c400'` 。 SELECT 语句的此部分将目标行与所有其他语句区分开来，因为 `CustomerID` 是目标表的主键。 WHERE 子句的信息从记录的原始版本（ `DataRowVersion.Original` ）派生而来，以防需要标识行的值已更改。

- 传输的 SQL 语句包含 SET 子句，用于设置已修改列的新值。

   > [!NOTE]
   > 如果 TableAdapter 的 `UpdateCommand` 属性已设置为存储过程的名称，则该适配器将不会构造 SQL 语句。 相反，它将调用具有传入的相应参数的存储过程。

## <a name="pass-parameters"></a>传递参数

通常使用参数来传递要在数据库中更新的记录的值。 当 TableAdapter 的 `Update` 方法运行 UPDATE 语句时，它需要填写参数值。 它从 `Parameters` 相应的数据命令（在本例中为 TableAdapter 中的对象）的集合中获取这些值 `UpdateCommand` 。

如果已使用 Visual Studio 工具生成数据适配器，则对象将包含与 `UpdateCommand` 语句中的每个参数占位符对应的参数集合。

<xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A?displayProperty=fullName>每个参数的属性指向数据表中的列。 例如， `SourceColumn` `au_id` 和参数的属性 `Original_au_id` 设置为数据表中包含作者 id 的任何列。适配器的 `Update` 方法运行时，它将从正在更新的记录中读取作者 id 列，并将值填充到语句中。

在 UPDATE 语句中，您需要同时指定新值（将写入记录的值）和旧值（以便记录可以位于数据库中）。 因此，每个值都有两个参数：一个用于 SET 子句，另一个用于 WHERE 子句。 这两个参数都从正在更新的记录中读取数据，但它们基于参数的属性获取不同版本的列值 <xref:System.Data.SqlClient.SqlParameter.SourceVersion> 。 SET 子句的参数获取当前版本，WHERE 子句的参数获取原始版本。

> [!NOTE]
> 你还可以在代码中自行设置集合中的值 `Parameters` ，你通常会在数据适配器事件的事件处理程序中执行此操作 <xref:System.Data.DataTable.RowChanging> 。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [创建和配置 TableAdapter](create-and-configure-tableadapters.md)
- [使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](validate-data-in-datasets.md)
- [如何：添加、修改和删除实体（WCF 数据服务）](/dotnet/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services)
