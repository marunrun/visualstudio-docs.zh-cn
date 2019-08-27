---
title: 将数据保存回数据库
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 31b41a9c18a9e055c9d144c7115d3673ee2e4443
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62566570"
---
# <a name="save-data-back-to-the-database"></a>将数据保存回数据库

数据集是数据的内存中副本。 如果您修改该数据，则最好将这些更改保存回数据库。 您实现这三种方式之一：

- 通过调用之一`Update`的 TableAdapter 方法

- 通过调用之一`DBDirect`的 TableAdapter 方法

- 通过调用`UpdateAll`上数据集包含在数据集中的其他表相关的表时，Visual Studio 将生成为你 TableAdapterManager 方法

当你的数据绑定到 Windows 窗体或 XAML 页面上的控件的数据集表时，数据绑定体系结构为您做所有工作。

如果您熟悉使用 Tableadapter，您可以直接跳转到以下主题之一：

|主题|描述|
|-----------|-----------------|
|[将新记录插入数据库](../data-tools/insert-new-records-into-a-database.md)|如何执行更新和插入使用 Tableadapter 或命令对象|
|[使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)|如何执行与 Tableadapter 的更新|
|[分层更新](../data-tools/hierarchical-update.md)|如何从具有两个或多个相关表的数据集执行的更新|
|[处理并发异常](../data-tools/handle-a-concurrency-exception.md)|如何在两个用户尝试同时更改相同的数据在数据库中时处理异常|
|[如何：使用事务保存数据](../data-tools/save-data-by-using-a-transaction.md)|如何将数据保存在事务中使用的系统。 事务命名空间和 TransactionScope 对象|
|[将数据保存在事务中](../data-tools/save-data-in-a-transaction.md)|创建 Windows 窗体应用程序来演示保存到数据库在事务内的数据的演练|
|[将数据保存到数据库（多个表）](../data-tools/save-data-to-a-database-multiple-tables.md)|如何编辑记录并将更改保存回数据库的多个表中|
|[将数据从对象保存到数据库](../data-tools/save-data-from-an-object-to-a-database.md)|如何将数据传递到数据库的数据集在不是使用 TableAdapter DbDirect 方法的对象从|
|[用 TableAdapter DBDirect 方法保存数据](../data-tools/save-data-with-the-tableadapter-dbdirect-methods.md)|如何使用 TableAdapter 直接向数据库发送 SQL 查询|
|[将数据集另存为 XML](../data-tools/save-a-dataset-as-xml.md)|如何将数据集保存到 XML 文档|

## <a name="two-stage-updates"></a>两阶段更新

更新数据源是一个两步过程。 第一步是使用新记录、 已更改的记录或已删除的记录更新该数据集。 如果你的应用程序永远不会将这些更改发送回数据源，您就完成了更新。

如果执行操作将更改发送回数据库，则需要第二个步骤。 如果不使用数据绑定控件，则必须手动调用`Update`同一 TableAdapter （或数据适配器） 的方法，用于填充数据集。 但是，若要将数据从一个数据源移到另一个，或更新多个数据源，还可以使用不同的适配器，例如。 如果不使用数据绑定，并且保存相关表的更改，则必须手动实例化自动生成的变量`TableAdapterManager`类，然后调用其`UpdateAll`方法。

![数据集更新的概念图](../data-tools/media/vbdatasetupdates.gif)

数据集包含的表，其中包含的行集合的集合。 如果想要以后更新基础数据源，则必须在使用方法`DataTable.DataRowCollection`属性添加或删除行时。 这些方法执行更改跟踪所必需的数据源进行更新。 如果调用`RemoveAt`集合上的行属性中，删除不会发送回数据库。

## <a name="merge-datasets"></a>合并数据集

可以更新的数据集内容*合并*其与另一个数据集。 这涉及到复制的内容*源*到调用数据集中的数据集 (称为*目标*数据集)。 合并数据集后，将源数据集的新记录添加到目标数据集。 此外，源数据集中的额外列添加到目标数据集。 合并数据集时，有一个本地的数据集和其他应用程序中获取第二个数据集。 当从 XML web 服务，例如组件获取第二个数据集时或当您需要集成来自多个数据集的数据时还有很有用。

当合并数据集，您可以传递布尔参数 (`preserveChanges`)，它告诉<xref:System.Data.DataSet.Merge%2A>方法是否保留在目标数据集中的现有修改。 由于数据集维护记录的多个版本，务必要时刻牢记合并多个记录的版本。 下表显示了如何合并两个数据集中的记录：

|DataRowVersion|目标数据库|源数据集|
| - | - | - |
|原始|James Wilson|James C. Wilson|
|当前|Jim Wilson|James C. Wilson|

调用<xref:System.Data.DataSet.Merge%2A>方法使用了上表`preserveChanges=false targetDataset.Merge(sourceDataset)`将导致以下数据：

|DataRowVersion|目标数据库|源数据集|
| - | - | - |
|原始|James C. Wilson|James C. Wilson|
|当前|James C. Wilson|James C. Wilson|

调用<xref:System.Data.DataSet.Merge%2A>方法替换`preserveChanges = true targetDataset.Merge(sourceDataset, true)`将导致以下数据：

|DataRowVersion|目标数据库|源数据集|
| - | - | - |
|原始|James C. Wilson|James C. Wilson|
|当前|Jim Wilson|James C. Wilson|

> [!CAUTION]
> 在中`preserveChanges = true`方案中，如果<xref:System.Data.DataSet.RejectChanges%2A>在目标数据集中，记录上调用方法，则它将恢复为原始数据从*源*数据集。 这意味着，如果你尝试更新原始数据源与目标数据集，它可能不能以查找要更新的原始行。 通过使用数据源的已更新的记录填充另一个数据集，然后执行合并来防止并发冲突，可以防止并发冲突。 （另一个用户修改数据源中的记录后填充数据集时出现的并发冲突。）

## <a name="update-constraints"></a>更新约束

若要对现有的数据行进行更改，添加或更新单个列中的数据。 如果数据集包含约束 （如外键或不可以为 null 的约束），就可以记录可以暂时将处于错误状态在更新。 也就是说，它可以是处于错误状态在完成更新一列之后，但之前获取的下一个。

为了避免过早约束冲突可以暂时挂起更新约束。 这有两个用途：

- 它会阻止在已完成更新一列，但尚未启动的另一个更新后引发错误。

- 它可防止某些更新来自正在事件引发 （通常用于验证的事件）。

> [!NOTE]
> 在 Windows 窗体中数据网格中内置的数据绑定体系结构挂起约束检查，直到焦点移出一个行，并不需要显式调用<xref:System.Data.DataRow.BeginEdit%2A>， <xref:System.Data.DataRow.EndEdit%2A>，或<xref:System.Data.DataRow.CancelEdit%2A>方法。

约束会自动禁用时<xref:System.Data.DataSet.Merge%2A>数据集上调用方法。 合并完成后，如果无法启用对数据集的任何约束<xref:System.Data.ConstraintException>引发。 在此情况下，<xref:System.Data.DataSet.EnforceConstraints%2A>属性设置为`false,`和重置之前，必须解决所有约束冲突<xref:System.Data.DataSet.EnforceConstraints%2A>属性设置为`true`。

完成更新后，可以重新启用约束检查，还将重新启用更新事件并引发它们。

有关挂起事件的详细信息，请参阅[填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

## <a name="dataset-update-errors"></a>数据集更新错误

更新在数据集中的记录时可能出现错误。 例如，可能会无意中编写到列、 错误类型的数据或数据太长或具有一些其他完整性问题的数据。 或者，你可能可以在任何阶段更新事件过程中引发自定义错误的特定于应用程序的验证检查。 有关详细信息，请参阅[验证数据集中](../data-tools/validate-data-in-datasets.md)。

## <a name="maintain-information-about-changes"></a>维护有关更改的信息

有关在数据集中的更改的信息保留在两种方式： 通过标记指示它们已更改的行 (<xref:System.Data.DataRow.RowState%2A>)，以及通过保留一条记录的多个副本 (<xref:System.Data.DataRowVersion>)。 通过使用此信息，进程可以确定所发生的更改在数据集中，并且可以将相应更新发送到数据源。

### <a name="rowstate-property"></a>RowState 属性

<xref:System.Data.DataRow.RowState%2A>属性的<xref:System.Data.DataRow>对象是一个值，提供有关特定数据行的状态信息。

下表详细说明的可能值<xref:System.Data.DataRowState>枚举：

|DataRowState 值|描述|
| - |-----------------|
|<xref:System.Data.DataRowState.Added>|行添加到的项作为<xref:System.Data.DataRowCollection>。 (处于此状态的行不具有相应的原始版本，因为它不存在时最后一个<xref:System.Data.DataRow.AcceptChanges%2A>调用方法)。|
|<xref:System.Data.DataRowState.Deleted>|使用已删除该行<xref:System.Data.DataRow.Delete%2A>的<xref:System.Data.DataRow>对象。|
|<xref:System.Data.DataRowState.Detached>|该行已创建，但不属于任何<xref:System.Data.DataRowCollection>。 一个<xref:System.Data.DataRow>对象在立即创建后，之前它已添加到一个集合，并已从集合中删除它后处于此状态。|
|<xref:System.Data.DataRowState.Modified>|以某种方式已更改的行中列的值。|
|<xref:System.Data.DataRowState.Unchanged>|以来未更改行<xref:System.Data.DataRow.AcceptChanges%2A>上一次调用。|

### <a name="datarowversion-enumeration"></a>DataRowVersion 枚举

数据集维护记录的多个版本。 <xref:System.Data.DataRowVersion>检索的值中找到时使用字段<xref:System.Data.DataRow>使用<xref:System.Data.DataRow.Item%2A>属性或<xref:System.Data.DataRow.GetChildRows%2A>方法<xref:System.Data.DataRow>对象。

下表详细说明的可能值<xref:System.Data.DataRowVersion>枚举：

|DataRowVersion 值|描述|
| - |-----------------|
|<xref:System.Data.DataRowVersion.Current>|一条记录的当前版本包含在上次记录执行的所有修改<xref:System.Data.DataRow.AcceptChanges%2A>调用。 如果行已被删除，则没有当前版本。|
|<xref:System.Data.DataRowVersion.Default>|一条记录，定义数据集架构或数据源的默认值。|
|<xref:System.Data.DataRowVersion.Original>|一条记录的原始版本是记录的副本，因为它是最后一次提交更改时在数据集中。 实际上，这通常是一条记录的版本为已读从数据源。|
|<xref:System.Data.DataRowVersion.Proposed>|正在更新时暂时可用的记录的建议的版本 — 也就是说，这段时间你调用<xref:System.Data.DataRow.BeginEdit%2A>方法和<xref:System.Data.DataRow.EndEdit%2A>方法。 您通常访问的事件处理程序中的记录的建议的版本如<xref:System.Data.DataTable.RowChanging>。 调用<xref:System.Data.DataRow.CancelEdit%2A>方法反转所做的更改和删除数据行的提议的版本。|

更新信息将传送到数据源时，原始和当前版本很有用。 通常情况下，当更新发送到数据源，为数据库的新信息是一条记录的当前版本中。 与原始版本的信息用于查找要更新的记录。

例如，在其中更改记录的主键的情况下，您需要一种方法，以在数据源中查找正确的记录，以便更新所做的更改。 如果没有原始版本已存在，则很可能会将记录追加到数据源，从而不仅在额外的多余的记录，而且是不准确和过期的一个记录中。 两个版本也用于在并发控制。 您可以比较针对要确定是否已更改记录，因为它已加载到数据集的数据源中的记录的原始版本。

建议的版本时，您需要执行实际提交到数据集所做的更改之前验证。

即使记录已发生更改，存在并不总是该行的原始或当前版本。 时该表中插入新行，没有原始版本，只有当前版本。 同样，如果删除的行通过调用表的`Delete`方法，初始版本，但没有当前版本。

您可以对其进行测试以查看记录的特定版本是否存在通过查询数据行的<xref:System.Data.DataRow.HasVersion%2A>方法。 可以通过传递访问记录的任一版本<xref:System.Data.DataRowVersion>枚举值作为请求的列的值时的可选参数。

## <a name="get-changed-records"></a>获取已更改的记录

它是常见的做法，不能更新在数据集中的每个记录。 例如，用户可能使用 Windows 窗体<xref:System.Windows.Forms.DataGridView>控件，用于显示多个记录。 但是，用户可能更新仅几条记录，删除其中一个，并插入一个新。 数据集和数据的表提供了一种方法 (`GetChanges`) 用于返回已修改的行。

可以创建使用已更改的记录的子集`GetChanges`数据表的方法 (<xref:System.Data.DataTable.GetChanges%2A>) 或数据集 (<xref:System.Data.DataSet.GetChanges%2A>) 本身。 如果对数据表调用该方法，它将返回具有已更改的记录的表的副本。 同样，如果在数据集上调用该方法，则在其中收到具有已更改的记录的新数据集。

`GetChanges` 本身返回的所有已更改的记录。 与此相反，通过传递所需<xref:System.Data.DataRowState>作为参数`GetChanges`方法，可以指定何种所需的更改记录子集： 新添加的记录，记录标记为删除，分离记录，或修改记录。

获取已更改的记录的子集时，你想要将记录发送到另一个组件进行处理。 而不是发送整个数据集，您可以减少通过获取该组件需要的记录与其他组件进行通信的开销。

## <a name="commit-changes-in-the-dataset"></a>提交数据集中的更改

在数据集中，做出更改后<xref:System.Data.DataRow.RowState%2A>属性已更改行的设置。 建立、 维护和供你的原始版本和当前版本记录<xref:System.Data.DataRowView.RowVersion%2A>属性。 存储在这些已更改行的属性的元数据，才将正确的更新发送到数据源。

如果所做的更改反映数据源的当前状态，不再需要维护该信息。 通常情况下，有两次时将数据集和其源是保持同步：

- 立即后已将信息加载到数据集，如从源读取数据时。

- 将更改从数据集发送到数据源之后 (而不是之前，因为可能会损失将更改发送到数据库所需的更改信息)。

您可以通过调用挂起的更改提交到数据集<xref:System.Data.DataSet.AcceptChanges%2A>方法。 通常情况下，<xref:System.Data.DataSet.AcceptChanges%2A>调用在以下时间：

- 将数据集加载之后。 如果加载数据集通过调用 TableAdapter 的`Fill`方法，则适配器会自动为您提交更改。 但是，如果通过将另一个数据集合并到它加载数据集，然后你必须手动提交所做的更改。

    > [!NOTE]
    > 可以防止自动提交所做的更改时调用适配器`Fill`方法通过设置`AcceptChangesDuringFill`适配器添加到属性`false`。 如果设置为`false`，则<xref:System.Data.DataRow.RowState%2A>的每个填充过程中插入的行设置为<xref:System.Data.DataRowState.Added>。

- 之后将数据集更改发送到另一个进程，如 XML web 服务。

    > [!CAUTION]
    > 这种方法提交更改，则会删除任何更改信息。 不提交后的更改直到您完成执行的操作所要求应用程序知道在数据集中进行了哪些更改。

此方法完成以下任务：

- 将写入<xref:System.Data.DataRowVersion.Current>版本记录到其<xref:System.Data.DataRowVersion.Original>版本并覆盖原始版本。

- 删除任何行位置<xref:System.Data.DataRow.RowState%2A>属性设置为<xref:System.Data.DataRowState.Deleted>。

- 集<xref:System.Data.DataRow.RowState%2A>属性的一条记录<xref:System.Data.DataRowState.Unchanged>。

<xref:System.Data.DataSet.AcceptChanges%2A>方法提供了三个级别。 你可以对调用<xref:System.Data.DataRow>到提交对象更改只是该行。 您还可以在调用它<xref:System.Data.DataTable>对象提交表中的所有行。 最后，在调用它<xref:System.Data.DataSet>对象提交的数据集的所有表的所有记录中所有挂起的更改。

下表描述了所提交的更改基于何种对象上调用该方法：

|方法|结果|
|------------|------------|
|<xref:System.Data.DataRow.AcceptChanges%2A?displayProperty=fullName>|仅在特定的行上提交更改。|
|<xref:System.Data.DataTable.AcceptChanges%2A?displayProperty=fullName>|中的特定表的所有行都提交的更改。|
|<xref:System.Data.DataSet.AcceptChanges%2A?displayProperty=fullName>|提交的数据集的所有表中的所有行的更改。|

> [!NOTE]
> 如果加载数据集通过调用 TableAdapter 的`Fill`方法，您不必显式接受更改。 默认情况下`Fill`方法调用`AcceptChanges`后完成填充数据表的方法。

相关的方法<xref:System.Data.DataSet.RejectChanges%2A>，通过复制来撤消更改的影响<xref:System.Data.DataRowVersion.Original>回版本<xref:System.Data.DataRowVersion.Current>的记录的版本。 它还设置<xref:System.Data.DataRow.RowState%2A>的每个记录回到<xref:System.Data.DataRowState.Unchanged>。

## <a name="data-validation"></a>数据验证

若要验证你的应用程序中的数据满足的要求将它传递到的进程，通常需要添加验证。 这样做可能会检查窗体中用户的条目正确，验证发送到另一个应用程序，应用程序的数据或甚至检查在组件中计算的信息位于你的数据源的约束内和应用程序要求。

你可以验证几种方法中的数据：

- 在业务层，通过将代码添加到应用程序以验证数据。 数据集是一个可以执行此操作的位置。 数据集提供了一些后端验证的优点，例如验证更改，如列和行的值变化的能力。 有关详细信息，请参阅[验证数据集中](../data-tools/validate-data-in-datasets.md)。

- 中的表示层，通过将验证添加到窗体。 有关详细信息，请参阅[用户输入 Windows 窗体中的验证](/dotnet/framework/winforms/user-input-validation-in-windows-forms)。

- 数据在后端，通过将数据发送到数据源 — 例如，数据库，并使其能够接受或拒绝数据。 如果您正在使用的数据库，具有复杂的功能来验证数据并提供错误的信息，这可以是一个实用的方法，因为可以验证无论它是从哪里的数据。 但是，这种方法可能不适合特定于应用程序的验证要求。 此外，让数据源验证数据可能会导致大量的往返到数据源，具体取决于你的应用程序如何由后端引发的验证错误的解决方法。

   > [!IMPORTANT]
   > 使用与数据命令时<xref:System.Data.SqlClient.SqlCommand.CommandType%2A>属性设置为<xref:System.Data.CommandType.Text>，仔细检查并向其传递到数据库之前从客户端发送的信息。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 将内容传输到数据库的用户输入之前，始终验证信息有效。 它是始终使用参数化的查询或存储的过程时可能是最佳做法。

## <a name="transmit-updates-to-the-data-source"></a>传输到数据源的更新

在数据集中进行了更改后，可以传输到数据源的更改。 大多数情况下，执行此操作通过调用`Update`TableAdapter （或数据适配器） 的方法。 该方法将遍历每个表中记录数据，确定所需的更新的类型 （更新、 插入或删除） (如果有） 并运行相应命令。

为举例说明了如何进行更新，假设应用程序使用包含单个数据表的数据集。 应用程序从数据库提取两个行。 在检索之后，内存中数据的表如下所示：

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Unchanged)    c400         Nancy Buchanan    Pending
```

你的应用程序将 Nancy Buchanan 状态更改为"首选。" 由于此更改的值<xref:System.Data.DataRow.RowState%2A>属性为该行从更改<xref:System.Data.DataRowState.Unchanged>到<xref:System.Data.DataRowState.Modified>。 值<xref:System.Data.DataRow.RowState%2A>属性的第一行将保持<xref:System.Data.DataRowState.Unchanged>。 数据表现在如下所示：

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Modified)     c400         Nancy Buchanan    Preferred
```

应用程序现在调用 `Update` 方法，将数据集传送给数据库。 该方法又会检查每个行。 对于第一个行，方法传送到数据库任何 SQL 语句，因为最初从数据库提取该行未更改。

对于第二个行，但是，`Update`方法自动调用正确的数据命令，并将其传输到数据库。 SQL 语句的特定语法取决于基础数据存储所支持的 SQL 的方言。 但是，传送的 SQL 语句的以下常规特征是值得注意的内容：

- 传送的 SQL 语句是 UPDATE 语句。 适配器知道使用 UPDATE 语句，因为值<xref:System.Data.DataRow.RowState%2A>属性是<xref:System.Data.DataRowState.Modified>。

- 传送的 SQL 语句包含 WHERE 子句的 UPDATE 语句的目标行，该值指示在其中`CustomerID = 'c400'`。 SELECT 语句的此部分使目标行有别于其他所有因为`CustomerID`是目标表的主键。 WHERE 子句派生自该记录的原始版本的信息 (`DataRowVersion.Original`)、 所需标识行的值已更改的情况下。

- 传输的 SQL 语句包含 SET 子句，若要设置已修改的列的新值。

   > [!NOTE]
   > 如果 TableAdapter 的`UpdateCommand`属性已设置为存储过程的名称，该适配器并不会构造 SQL 语句。 相反，它与中的相应参数调用存储的过程。

## <a name="pass-parameters"></a>将参数传递

通常使用参数来传递要在数据库中更新的记录的值。 当 TableAdapter 的`Update`方法运行 UPDATE 语句，它需要通过填充参数值。 获取这些值从`Parameters`相应的数据命令的集合，在这种情况下， `UpdateCommand` TableAdapter 中的对象。

如果您已使用 Visual Studio 工具生成的数据适配器，`UpdateCommand`对象包含对应于在语句中的每个参数占位符的参数的集合。

<xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A?displayProperty=fullName>的每个参数的属性指向数据的表中的列。 例如，`SourceColumn`属性`au_id`和`Original_au_id`参数设置为数据表中的任意一列包含的作者 id。当适配器的`Update`方法运行时，它从读取作者 id 列正在更新并将值填充到语句中的记录。

在 UPDATE 语句中，您需要指定这两个新的值 （这些会写入到该记录） 以及旧值 （以便可以在数据库中位于该记录）。 有，因此，每个值的两个参数： 一个用于 SET 子句，另一个则用于 WHERE 子句。 这两个参数更新时，记录中读取数据，但它们获取基于参数的列值的不同版本<xref:System.Data.SqlClient.SqlParameter.SourceVersion>属性。 SET 子句的参数获取最新版本，并在 WHERE 子句的参数获取的原始版本。

> [!NOTE]
> 此外可以设置值`Parameters`集合中的数据适配器的事件处理程序中通常所执行的操作的代码中自行<xref:System.Data.DataTable.RowChanging>事件。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [创建和配置 Tableadapter](create-and-configure-tableadapters.md)
- [使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](validate-data-in-datasets.md)
- [如何：添加、 修改和删除实体 (WCF data services)](/dotnet/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services)