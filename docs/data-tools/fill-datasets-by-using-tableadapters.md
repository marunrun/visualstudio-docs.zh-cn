---
title: 使用 Tableadapter 填充数据集
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic]
- datasets [Visual Basic], loading data
- data retrieval
- retrieving data
- datasets [Visual Basic], filling
- data [Visual Studio], retrieving
- data [Visual Studio], datasets
ms.assetid: 55f3bfbe-db78-4486-add3-c62f49e6b9a0
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 888e2ac47348d7e61d115f51e3ea52d15ea9f447
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85282431"
---
# <a name="fill-datasets-by-using-tableadapters"></a>使用 Tableadapter 填充数据集

TableAdapter 组件根据指定的一个或多个查询或存储过程，使用数据库中的数据填充数据集。 Tableadapter 还可以对数据库执行添加、更新和删除操作，以便保存对数据集所做的更改。 还可以发出与任何特定表无关的全局命令。

> [!NOTE]
> Tableadapter 由 Visual Studio 设计器生成。 如果要以编程方式创建数据集，请使用 DataAdapter，这是一个 .NET 类。

有关 TableAdapter 操作的详细信息，可以直接跳到以下主题之一：

|主题|说明|
|-----------|-----------------|
|[创建和配置 TableAdapter](../data-tools/create-and-configure-tableadapters.md)|如何使用设计器创建和配置 Tableadapter|
|[创建参数化 TableAdapter 查询](../data-tools/create-parameterized-tableadapter-queries.md)|如何使用户能够为 TableAdapter 过程或查询提供参数|
|[使用 TableAdapter 直接访问数据库](../data-tools/directly-access-the-database-with-a-tableadapter.md)|如何使用 Tableadapter 的 Dbdirect 方法|
|[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|如何在更新数据时使用 foreign key 约束|
|[如何：扩展 TableAdapter 的功能](../data-tools/fill-datasets-by-using-tableadapters.md)|如何将自定义代码添加到 Tableadapter|
|[将 XML 数据读入数据集](../data-tools/read-xml-data-into-a-dataset.md)|如何使用 XML|

<a name="tableadapter-overview"></a>

## <a name="tableadapter-overview"></a>TableAdapter 概述

Tableadapter 是由设计器生成的组件，用于连接到数据库、运行查询或存储过程，并使用返回的数据填充其 DataTable。 Tableadapter 还会将更新的数据从应用程序发送回数据库。 可以在 TableAdapter 上运行任意多个查询，前提是这些查询返回的数据符合与 TableAdapter 关联的表的架构。 下图显示了 Tableadapter 如何与数据库和内存中的其他对象进行交互：

![客户端应用程序中的数据流](../data-tools/media/clientdatadiagram.gif)

尽管 Tableadapter 是用 **数据集设计器**设计的，但 TableAdapter 类不会生成为的嵌套类  <xref:System.Data.DataSet> 。 它们位于特定于每个数据集的不同命名空间中。 例如，如果你有一个名为的数据集 `NorthwindDataSet` ，则与中的关联的 tableadapter 将  <xref:System.Data.DataTable> `NorthwindDataSet` 在 `NorthwindDataSetTableAdapters` 命名空间中。 若要以编程方式访问特定 TableAdapter，必须声明 TableAdapter 的新实例。 例如：

[!code-csharp[VbRaddataTableAdapters#7](../data-tools/codesnippet/CSharp/fill-datasets-by-using-tableadapters_1.cs)]
[!code-vb[VbRaddataTableAdapters#7](../data-tools/codesnippet/VisualBasic/fill-datasets-by-using-tableadapters_1.vb)]

## <a name="associated-datatable-schema"></a>关联的 DataTable 架构

创建 TableAdapter 时，使用初始查询或存储过程来定义 TableAdapter 关联的架构 <xref:System.Data.DataTable> 。 您可以通过调用 TableAdapter 的 `Fill` 方法 (来填充 tableadapter 的关联) 来运行此初始查询或存储过程 <xref:System.Data.DataTable> 。 对 TableAdapter 的主查询所做的任何更改都会反映在关联数据表的架构中。 例如，从主查询中删除列还会从关联的数据表中删除列。 如果针对 TableAdapter 的任何附加查询使用 SQL 语句来返回主查询中不存在的列，则设计器将尝试同步主查询与其他查询之间的列更改。

## <a name="tableadapter-update-commands"></a>TableAdapter 更新命令

TableAdapter 的更新功能取决于在 **Tableadapter 向导**的主查询中提供了多少信息。 例如，如果 Tableadapter 配置为从多个表中提取值 (使用 `JOIN`) 、标量值、视图或聚合函数的结果，则最初不会创建可将更新发送回基础数据库的功能。 但是，你可以 `INSERT` `UPDATE` `DELETE` 在 " **属性** " 窗口中手动配置、和命令。

## <a name="tableadapter-queries"></a>TableAdapter 查询

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

Tableadapter 可包含多个查询来填充关联的数据表。 您可以根据应用程序的需要为 TableAdapter 定义任意多个查询，前提是每个查询都返回与其关联数据表具有相同架构的数据。 此功能使 TableAdapter 能够根据不同的条件加载不同的结果。

例如，如果您的应用程序包含包含客户名称的表，则您可以创建一个查询，该查询使用以特定字母开头的每个客户名称来填充表，而另一个则使用处于相同状态的所有客户填充该表。 若要 `Customers` 使用处于给定状态的客户填充表，可以创建一个 `FillByState` 查询，该查询采用状态值的参数，如下所示： `SELECT * FROM Customers WHERE State = @State` 。 可以通过调用 `FillByState` 方法并传入参数值来运行查询，如下所示： `CustomerTableAdapter.FillByState("WA")` 。

除了添加返回与 TableAdapter 的数据表相同的架构数据的查询之外，还可以添加返回标量 (单个) 值的查询。 例如，返回 () 客户计数的查询 `SELECT Count(*) From Customers` 对于有效， `CustomersTableAdapter,` 即使返回的数据不符合表的架构。

## <a name="clearbeforefill-property"></a>ClearBeforeFill 属性

默认情况下，每次运行查询以填充 TableAdapter 的数据表时，现有数据会被清除，并且仅将查询的结果加载到表中。 `ClearBeforeFill` `false` 如果要将从查询返回的数据添加或合并到数据表中的现有数据，请将 TableAdapter 的属性设置为。 不管是否清除数据，都需要将更新显式发送回数据库（如果要保存这些更新）。 因此，请记住在运行填充表的另一个查询之前保存对表中数据所做的任何更改。 有关详细信息，请参阅 [使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。

## <a name="tableadapter-inheritance"></a>TableAdapter 继承

Tableadapter 通过封装配置的类来扩展标准数据适配器的功能 <xref:System.Data.Common.DataAdapter> 。 默认情况下，TableAdapter 从类继承 <xref:System.ComponentModel.Component> ，不能转换为 <xref:System.Data.Common.DataAdapter> 类。 将 TableAdapter 转换为 <xref:System.Data.Common.DataAdapter> 类会导致 <xref:System.InvalidCastException> 错误。 若要更改 TableAdapter 的基类，可以指定从 <xref:System.ComponentModel.Component> **数据集设计器**中的 Tableadapter 的 "**基类**" 属性派生的类。

## <a name="tableadapter-methods-and-properties"></a>TableAdapter 方法和属性

TableAdapter 类不是 .NET 类型。 这意味着不能在文档或 **对象浏览器**中查找。 它在设计时使用前面提到的向导之一创建。 根据所使用的表的名称，在创建时分配给 TableAdapter 的名称。 例如，基于名为的数据库中的表创建 TableAdapter 时 `Orders` ，tableadapter 的名称为 `OrdersTableAdapter` 。 可以使用**数据集设计器**中的 "**名称**" 属性更改 TableAdapter 的类名。

下面是 Tableadapter 的常用方法和属性：

|成员|说明|
|------------|-----------------|
|`TableAdapter.Fill`|用 TableAdapter 的命令的结果填充 TableAdapter 的关联数据表 `SELECT` 。|
|`TableAdapter.Update`|将更改发送回数据库，并返回一个整数，该整数表示受更新影响的行数。 有关详细信息，请参阅 [使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。|
|`TableAdapter.GetData`|返回填充了 <xref:System.Data.DataTable> 数据的新。|
|`TableAdapter.Insert`|在数据表中创建新行。 有关详细信息，请参阅在 [数据库中插入新记录](../data-tools/insert-new-records-into-a-database.md)。|
|`TableAdapter.ClearBeforeFill`|确定在调用方法之一之前是否清空数据表 `Fill` 。|

## <a name="tableadapter-update-method"></a>TableAdapter 更新方法

Tableadapter 使用数据命令从数据库中读取和写入数据。 使用 TableAdapter 的初始 `Fill` (main) 查询来创建关联数据表的架构，以及 `InsertCommand` `UpdateCommand` `DeleteCommand` 与方法相关联的、、和命令 `TableAdapter.Update` 。 调用 TableAdapter 的 `Update` 方法会运行最初配置 TableAdapter 时创建的语句，而不是使用 **TableAdapter 查询配置向导**添加的其他查询之一。

使用 TableAdapter 时，它会有效地执行与通常会执行的命令相同的操作。 例如，当您调用适配器的方法时 `Fill` ，适配器会在其属性中运行数据命令 `SelectCommand` 并使用数据读取器 (例如， <xref:System.Data.SqlClient.SqlDataReader>) 将结果集加载到数据表。 同样，在调用适配器的方法时 `Update` ，它会在 `UpdateCommand` 、 `InsertCommand` 和 `DeleteCommand` 属性) 为数据表中的每个已更改的记录运行相应的命令 (。

> [!NOTE]
> 如果主查询中有足够的信息，则 `InsertCommand` 默认情况下，在 `UpdateCommand` `DeleteCommand` 生成 TableAdapter 时，会创建、和命令。 如果 TableAdapter 的主查询多于单个表 `SELECT` 语句，设计器可能无法生成 `InsertCommand` 、 `UpdateCommand` 和 `DeleteCommand` 。 如果未生成这些命令，则在运行该方法时可能会收到错误 `TableAdapter.Update` 。

## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter GenerateDbDirectMethods

除了 `InsertCommand` 、和以外 `UpdateCommand` ，还 `DeleteCommand` 可以通过对数据库直接运行的方法创建 tableadapter。 可以直接调用这些方法 (`TableAdapter.Insert` 、 `TableAdapter.Update` 和 `TableAdapter.Delete`) ，以操作数据库中的数据。 这意味着你可以从代码中调用这些单独的方法，而不是调用 `TableAdapter.Update` 来处理为关联数据表挂起的插入、更新和删除操作。

如果不想创建这些直接方法，请在 "属性" 窗口中将 TableAdapter 的**GenerateDbDirectMethods**属性设置为 `false` () 。 **Properties** 添加到 TableAdapter 的其他查询是独立查询，它们不会生成这些方法。

## <a name="tableadapter-support-for-nullable-types"></a>TableAdapter 支持可以为 null 的类型

Tableadapter 支持可以为 null `Nullable(Of T)` 的类型和 `T?` 。 若要深入了解 Visual Basic 中可以为 null 的类型，请参阅[可以为 null 的值类型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)。 有关 c # 中可以为 null 的类型的详细信息，请参阅 [使用可以为 null 的类型](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。

<a name="tableadaptermanager-reference"></a>

## <a name="tableadaptermanager-reference"></a>TableAdapterManager 引用

默认情况下，当您创建包含相关表的数据集时，TableAdapterManager 类将生成。 若要防止生成类，请将 `Hierarchical Update` 数据集的属性值更改为 false。 将具有关系的表拖到 Windows 窗体或 WPF 页的设计图面上时，Visual Studio 将声明类的成员变量。 如果不使用数据绑定，则必须手动声明该变量。

TableAdapterManager 类不是 .NET 类型。 因此，您不能在文档中查找它。 它在设计时创建，作为数据集创建过程的一部分。

下面是类的常用方法和属性 `TableAdapterManager` ：

|成员|说明|
|------------|-----------------|
|`UpdateAll` 方法|保存所有数据表中的所有数据。|
|`BackUpDataSetBeforeUpdate` 属性|确定在执行方法之前是否创建数据集的备份副本 `TableAdapterManager.UpdateAll` 。变量.|
|*tableName* `TableAdapter` 知识产权|表示 TableAdapter。 生成的 TableAdapterManager 包含其管理的每个属性的属性 `TableAdapter` 。 例如，具有 Customers 和 Orders 表的数据集将生成包含和属性的 TableAdapterManager `CustomersTableAdapter` `OrdersTableAdapter` 。|
|`UpdateOrder` 属性|控制单个 insert、update 和 delete 命令的顺序。 将此项设置为枚举中的值之一 `TableAdapterManager.UpdateOrderOption` 。<br /><br /> 默认情况下， `UpdateOrder` 设置为 **InsertUpdateDelete**。 这意味着对数据集中的所有表执行 insert、update 和 delete 操作。|

## <a name="security"></a>安全性

如果使用的数据命令的 CommandType 属性设置为 <xref:System.Data.CommandType.Text> ，请在将客户端传递到数据库之前，仔细检查从该客户端发送的信息。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 将用户输入传输到数据库之前，请始终验证信息是否有效。 最佳做法是尽可能使用参数化查询或存储过程。

## <a name="see-also"></a>另请参阅

- [数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
