---
title: 使用 Tableadapter 填充数据集
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: a79f7b781944bb93a60794e748eefb9375723384
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301193"
---
# <a name="fill-datasets-by-using-tableadapters"></a>使用 Tableadapter 填充数据集

表适配器组件根据您指定的一个或多个查询或存储过程，使用数据库中的数据填充数据集。 表适配器还可以在数据库上执行添加、更新和删除，以保留对数据集所做的更改。 您还可以发出与任何特定表无关的全局命令。

> [!NOTE]
> 表适配器由可视化工作室设计器生成。 如果要以编程方式创建数据集，请使用 DataAdapter，这是一个 .NET 类。

有关表适配器操作的详细信息，您可以直接跳到以下主题之一：

|主题|说明|
|-----------|-----------------|
|[创建和配置 TableAdapter](../data-tools/create-and-configure-tableadapters.md)|如何使用设计器创建和配置表适配器|
|[创建参数化 TableAdapter 查询](../data-tools/create-parameterized-tableadapter-queries.md)|如何使用户能够向表适配器过程或查询提供参数|
|[使用 TableAdapter 直接访问数据库](../data-tools/directly-access-the-database-with-a-tableadapter.md)|如何使用表适配器的 Dbdirect 方法|
|[填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|更新数据时如何处理外键约束|
|[如何：扩展 TableAdapter 的功能](../data-tools/fill-datasets-by-using-tableadapters.md)|如何向表适配器添加自定义代码|
|[将 XML 数据读取到数据集中](../data-tools/read-xml-data-into-a-dataset.md)|如何使用 XML|

<a name="tableadapter-overview"></a>

## <a name="tableadapter-overview"></a>TableAdapter 概述

表适配器是设计器生成的组件，用于连接到数据库、运行查询或存储过程，并用返回的数据填充其 DataTable。 表适配器还会将更新的数据从应用程序发送回数据库。 只要在表适配器上返回符合表适配器关联的表的架构的数据，就可以在表适配器上运行所需的尽可能多的查询。 下图显示了表适配器如何与内存中的数据库和其他对象进行交互：

![客户端应用程序中的数据流](../data-tools/media/clientdatadiagram.gif)

虽然表适配器是使用**数据集设计器**设计的，但表适配器类不会生成为 嵌套类<xref:System.Data.DataSet>。 它们位于特定于每个数据集的单独命名空间中。 例如，`NorthwindDataSet`如果数据集名为 ，则 与<xref:System.Data.DataTable>中的 s 关联的表适配器`NorthwindDataSet`将位于命名空间中。 `NorthwindDataSetTableAdapters` 要以编程方式访问特定的表适配器，必须声明表适配器的新实例。 例如：

[!code-csharp[VbRaddataTableAdapters#7](../data-tools/codesnippet/CSharp/fill-datasets-by-using-tableadapters_1.cs)]
[!code-vb[VbRaddataTableAdapters#7](../data-tools/codesnippet/VisualBasic/fill-datasets-by-using-tableadapters_1.vb)]

## <a name="associated-datatable-schema"></a>关联的数据表架构

创建表适配器时，可以使用初始查询或存储过程来定义表适配器关联的<xref:System.Data.DataTable>架构。 通过调用表适配器`Fill`的方法（填充表适配器的关联<xref:System.Data.DataTable>），运行此初始查询或存储过程。 对表适配器的主查询所做的任何更改都反映在关联数据表的架构中。 例如，从主查询中删除列还会从关联的数据表中删除列。 如果表适配器上的任何其他查询都使用返回不在主查询中的列的 SQL 语句，则设计器将尝试同步主查询和其他查询之间的列更改。

## <a name="tableadapter-update-commands"></a>表适配器更新命令

表适配器的更新功能取决于**表适配器向导**中主查询中有多少信息可用。 例如，配置为从多个表（使用`JOIN`）标量值、视图或聚合函数的结果提取值的表适配器最初不会创建，并且能够将更新发送回基础数据库。 但是，您可以在 **"属性"** 窗口中`UPDATE`手动配置`DELETE``INSERT`和 命令。

## <a name="tableadapter-queries"></a>TableAdapter 查询

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

表适配器可以包含多个查询来填充其关联的数据表。 只要每个查询返回与其关联数据表相同的架构的数据，就可以根据应用程序的要求为表适配器定义尽可能多的查询。 此功能使表适配器能够根据不同的条件加载不同的结果。

例如，如果应用程序包含具有客户名称的表，则可以创建一个查询，该查询将表与以特定字母开头的每个客户名称填充，另一个查询将表与位于同一状态的所有客户填充。 要用给定`Customers`状态的客户填充表，可以创建一个`FillByState`查询，该查询获取状态值的参数，如下所示： `SELECT * FROM Customers WHERE State = @State`。 通过调用`FillByState`方法并传入如下所示的参数值来运行查询： `CustomerTableAdapter.FillByState("WA")`。

除了添加返回与表适配器的数据表相同的架构数据的查询外，还可以添加返回标量（单个）值的查询。 例如，返回客户计数 （`SELECT Count(*) From Customers`） 的查询对 有效，`CustomersTableAdapter,`即使返回的数据不符合表的架构。

## <a name="clearbeforefill-property"></a>清除之前填充属性

默认情况下，每次运行查询以填充表适配器的数据表时，都会清除现有数据，并且仅将查询的结果加载到表中。 如果要将从查询返回的数据`ClearBeforeFill`添加到数据`false`表中的现有数据，请将表适配器的属性设置为。 无论您是否清除数据，如果需要保留更新，则需要显式将更新发送回数据库。 因此，请记住在运行另一个填充表的查询之前保存对表中的数据的任何更改。 有关详细信息，请参阅[使用表适配器更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。

## <a name="tableadapter-inheritance"></a>表适配器继承

表适配器通过封装配置<xref:System.Data.Common.DataAdapter>的类来扩展标准数据适配器的功能。 默认情况下，表适配器从<xref:System.ComponentModel.Component>类继承，不能强制转换为<xref:System.Data.Common.DataAdapter>类。 将表适配器强制转换到<xref:System.Data.Common.DataAdapter>类会导致错误<xref:System.InvalidCastException>。 要更改表适配器的基类，可以在<xref:System.ComponentModel.Component>**数据集设计器**中的表适配器**的基类**属性中指定派生的类。

## <a name="tableadapter-methods-and-properties"></a>表适配器方法和属性

表适配器类不是 .NET 类型。 这意味着您无法在文档或**对象浏览器**中查找它。 它是在设计时创建的，当您使用前面提到的向导之一时。 创建表适配器时分配给它的名称基于您正在使用的表的名称。 例如，当您基于名为`Orders`的数据库中的表时，表适配器名为`OrdersTableAdapter`。 可以使用**数据集设计器**中的**Name**属性更改表适配器的类名称。

以下是表适配器的常用方法和属性：

|成员|说明|
|------------|-----------------|
|`TableAdapter.Fill`|使用表适配器`SELECT`的命令结果填充表适配器的关联数据表。|
|`TableAdapter.Update`|将更改发送回数据库并返回表示受更新影响的行数的整数。 有关详细信息，请参阅[使用表适配器更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。|
|`TableAdapter.GetData`|返回充满数据<xref:System.Data.DataTable>的新。|
|`TableAdapter.Insert`|在数据表中创建新行。 有关详细信息，请参阅[将新记录插入数据库](../data-tools/insert-new-records-into-a-database.md)。|
|`TableAdapter.ClearBeforeFill`|在调用其中一`Fill`种方法之前，确定数据表是否已清空。|

## <a name="tableadapter-update-method"></a>表适配器更新方法

表适配器使用数据命令从数据库读取和写入。 使用 TableAdapter`Fill`的初始（主）查询作为创建关联数据表以及`InsertCommand`与`UpdateCommand``DeleteCommand``TableAdapter.Update`方法关联的 的 的 和 命令的架构的基础。 调用表适配器`Update`的方法运行最初配置表适配器时创建的语句，而不是使用**表适配器查询配置向导**添加的其他查询之一。

使用表适配器时，它会使用通常执行的命令执行相同的操作。 例如，当您调用适配器`Fill`的方法时，适配器在其`SelectCommand`属性中运行数据命令，<xref:System.Data.SqlClient.SqlDataReader>并使用数据读取器（例如），将结果集加载到数据表中。 同样，当您调用`Update`适配器的方法时，它会为数据表中的每个已更改的记录运行相应的命令（`UpdateCommand`在`InsertCommand`和`DeleteCommand`属性中）。

> [!NOTE]
> 如果主查询中有足够的信息，则默认情况下生成表`InsertCommand`适配器`UpdateCommand`时将`DeleteCommand`创建 和 命令。 如果 TableAdapter 的主查询不仅仅是单个`SELECT`表语句，则设计器可能无法生成`InsertCommand`和`UpdateCommand`。 `DeleteCommand` 如果未生成这些命令，则在运行`TableAdapter.Update`该方法时可能会收到错误。

## <a name="tableadapter-generatedbdirectmethods"></a>表适配器生成Dbdirect方法

除了`InsertCommand`，`UpdateCommand`和`DeleteCommand`， 表适配器是使用可以直接针对数据库运行的方法创建的。 您可以直接调用这些方法 （`TableAdapter.Insert` `TableAdapter.Update`、`TableAdapter.Delete`和 ） 来操作数据库中的数据。 这意味着可以从代码调用这些单独的方法，而不是调用`TableAdapter.Update`以处理关联数据表挂起的插入、更新和删除。

如果不想创建这些直接方法，请将表适配器的 **"生成DbDirect方法**"属性设置为`false`（在 **"属性"** 窗口中）。 添加到表适配器的其他查询是独立查询 - 它们不会生成这些方法。

## <a name="tableadapter-support-for-nullable-types"></a>表适配器支持可消除类型

表适配器支持空类型`Nullable(Of T)`和`T?`。 若要深入了解 Visual Basic 中可以为 null 的类型，请参阅[可以为 null 的值类型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)。 有关 C# 中可 null 类型的详细信息，请参阅[使用空类型](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。

<a name="tableadaptermanager-reference"></a>

## <a name="tableadaptermanager-reference"></a>表适配器管理器引用

默认情况下，在创建包含相关表的数据集时，将生成表适配器管理器类。 为了防止生成类，将数据集`Hierarchical Update`的属性的值更改为 false。 将具有关系的表拖动到 Windows 窗体或 WPF 页的设计图面上时，Visual Studio 将声明类的成员变量。 如果不使用数据绑定，必须手动声明变量。

表适配器管理器类不是 .NET 类型。 因此，您不能在文档中查找它。 它是在设计时创建的，作为数据集创建过程的一部分。

以下是`TableAdapterManager`类的常用方法和属性：

|成员|说明|
|------------|-----------------|
|`UpdateAll` 方法|从所有数据表中保存所有数据。|
|`BackUpDataSetBeforeUpdate` 属性|确定在执行`TableAdapterManager.UpdateAll`方法之前是否创建数据集的备份副本。布尔。|
|*表名称*`TableAdapter`属性|表示 TableAdapter。 生成的表适配器管理器包含它管理的每个`TableAdapter`属性。 例如，具有客户和订单表的数据集使用包含 和`CustomersTableAdapter``OrdersTableAdapter`属性的表适配器管理器生成。|
|`UpdateOrder` 属性|控制各个插入、更新和删除命令的顺序。 将此设置为枚举中`TableAdapterManager.UpdateOrderOption`的值之一。<br /><br /> 默认情况下，`UpdateOrder`设置为**插入更新删除**。 这意味着对数据集中的所有表执行插入、更新和删除。|

## <a name="security"></a>安全性

将数据命令与 CommandType 属性设置为<xref:System.Data.CommandType.Text>时，请仔细检查从客户端发送的信息，然后再将其传递到数据库。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 在将用户输入传输到数据库之前，请始终验证信息是否有效。 最佳做法是尽可能始终使用参数化查询或存储过程。

## <a name="see-also"></a>另请参阅

- [数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
