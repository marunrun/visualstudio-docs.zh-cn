---
title: 使用 Tableadapter 填充数据集 |Microsoft Docs
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
- datasets [Visual Basic]
- datasets [Visual Basic], loading data
- data retrieval
- retrieving data
- datasets [Visual Basic], filling
- data [Visual Studio], retrieving
- data [Visual Studio], datasets
ms.assetid: 55f3bfbe-db78-4486-add3-c62f49e6b9a0
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fb06c1d97c854aae05d993c086069e10e35518f5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704973"
---
# <a name="fill-datasets-by-using-tableadapters"></a>使用 Tableadapter 填充数据集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TableAdapter 组件填充数据库，基于一个或多个查询或您指定的存储的过程中的数据的数据集。 Tableadapter 还可以执行添加、 更新和删除数据库来保存对数据集所做的更改。 此外可以颁发任何特定表，该表不相关的全局命令。  
  
> [!NOTE]
> Tableadapter 是由 Visual Studio 设计器生成的。 如果要以编程方式创建数据集，然后使用 DataAdapter，这是.NET Framework 类。  
  
 TableAdapter 操作有关的详细信息，您可以直接跳到以下主题之一：  
  
|主题|描述|  
|-----------|-----------------|  
|[创建和配置 Tableadapter](../data-tools/create-and-configure-tableadapters.md)|如何使用设计器创建和配置 Tableadapter|  
|[创建参数化 TableAdapter 查询](../data-tools/create-parameterized-tableadapter-queries.md)|如何使用户能够为 TableAdapter 过程或查询提供参数|  
|[使用 TableAdapter 直接访问数据库](../data-tools/directly-access-the-database-with-a-tableadapter.md)|如何使用 Tableadapter 的 Dbdirect 方法|  
|[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|如何更新数据时使用 foreign key 约束|  
|[如何：扩展 TableAdapter 的功能](../data-tools/fill-datasets-by-using-tableadapters.md)|如何将自定义代码添加到 Tableadapter|  
|[将 XML 数据读入到数据集中](../data-tools/read-xml-data-into-a-dataset.md)|如何使用 XML|  
  
## <a name="tableadapters-overview"></a>TableAdapter 概述  
 Tableadapter 是设计器生成的组件，连接到数据库、 运行的查询或存储的过程，并使用返回的数据填充其 DataTable。 Tableadapter 还从你的应用程序与数据库发送更新后的数据。 你可以运行尽可能多的查询，因为你想在 TableAdapter 上，只要它们符合的数据返回到 TableAdapter 与之关联的表的架构。 下图显示了 Tableadapter 如何与数据库和内存中的其他对象进行交互：  
  
 ![客户端应用程序中的数据流](../data-tools/media/clientdatadiagram.gif "ClientDataDiagram")  
  
 Tableadapter 的设计时**数据集设计器**，不会作为嵌套类的生成的 TableAdapter 类<xref:System.Data.DataSet>。 它们位于特定于每个数据集的单独命名空间中。 例如，如果您有一个名为的数据集`NorthwindDataSet`，与关联的 Tableadapter<xref:System.Data.DataTable>中的 s`NorthwindDataSet`会采用`NorthwindDataSetTableAdapters`命名空间。 若要以编程方式访问特定的 TableAdapter，您必须声明 TableAdapter 的新实例。 例如：  
  
 [!code-csharp[VbRaddataTableAdapters#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Class1.cs#7)]
 [!code-vb[VbRaddataTableAdapters#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Class1.vb#7)]  
  
## <a name="associated-datatable-schema"></a>关联的 DataTable 架构  
 使用初始查询或存储的过程定义 TableAdapter 的架构的关联来创建 TableAdapter 时<xref:System.Data.DataTable>。 运行此初始查询或通过调用 TableAdapter 的存储过程`Fill`方法 (它将填充 TableAdapter 的关联<xref:System.Data.DataTable>)。 TableAdapter 的主查询所做的任何更改都反映在关联的数据的表的架构。 例如，从主查询中删除列还将列从表中删除关联的数据。 如果在 TableAdapter 上的任何其他查询使用返回不在主查询中的列的 SQL 语句，在设计器会尝试同步主查询和其他查询之间的列更改。 有关详细信息，请参阅[如何：编辑 Tableadapter](https://msdn.microsoft.com/library/ca178745-e35a-45f1-a395-23cddfd8f855)。  
  
## <a name="tableadapter-update-commands"></a>TableAdapter 更新命令  
 TableAdapter 的更新功能是依赖于 TableAdapter 向导中的主查询中提供了多少信息。 例如，配置为提取多个表 （联接） 中的值、 标量值、 视图或聚合函数的结果的 Tableadapter 最初创建时不能够将更新发送回基础数据库。 但是，可以配置的 INSERT、 UPDATE 和 DELETE 命令中手动**属性**窗口。  
  
## <a name="tableadapter-queries"></a>TableAdapter 查询  
 ![使用多个查询的 TableAdapter](../data-tools/media/tableadapter.gif "TableAdapter")  
  
 Tableadapter 可包含多个查询以填充其关联的数据的表。 可以定义任意多个查询的 TableAdapter，因为应用程序需要，只要每个查询返回到其关联的数据的表相同的架构数据的架构。 此功能提供 TableAdapter 加载不同的结果基于不同条件。  
  
 例如，如果你的应用程序包含具有客户名称的表，您可以创建填充以某些字母开头的每个客户名称，另一个表都位于相同的状态的所有客户用填充表的查询。 若要填充`Customers`表与某一给定状态中的客户，可以创建`FillByState`采用的州值参数，如下所示的查询： `SELECT * FROM Customers WHERE State = @State`。 通过调用运行查询`FillByState`方法并传入参数值如下： `CustomerTableAdapter.FillByState("WA")`。  
  
 除了添加返回的 TableAdapter 的数据表的架构相同的数据的查询，可以添加返回标量 （单个） 值的查询。 例如，返回的客户计数的查询 (`SELECT Count(*) From Customers`) 对有效`CustomersTableAdapter,`即使返回的数据不符合到表的架构。  
  
## <a name="clearbeforefill-property"></a>ClearBeforeFill 属性  
 默认情况下，每次运行查询以填充 TableAdapter 的数据表，清除现有数据，并仅在查询结果加载到表。 设置 TableAdapter`ClearBeforeFill`属性设置为`false`如果想要添加或合并到数据表中的现有数据从查询返回的数据。 无论是否清除了数据，都需要显式将更新发送回数据库中，如果你想要保留它们。 因此请务必先运行填充表的另一个查询之前将任何更改保存到表中的数据。 有关详细信息，请参阅[使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。  
  
## <a name="tableadapter-inheritance"></a>TableAdapter 继承  
 Tableadapter 扩展标准数据适配器的功能通过封装一个已配置<xref:System.Data.Common.DataAdapter>类？ qualifyHint = False 和自动升级 = True。 默认情况下，TableAdapter 继承<xref:System.ComponentModel.Component>类，并不能强制转换为<xref:System.Data.Common.DataAdapter>类。 强制转换到 TableAdapter<xref:System.Data.Common.DataAdapter>类中的结果<xref:System.InvalidCastException>错误？ qualifyHint = False 和自动升级 = True。 若要更改的 TableAdapter 的基类，可以键入派生的类<xref:System.ComponentModel.Component>中**基类**属性中对 TableAdapter**数据集设计器**。  
  
## <a name="tableadapter-methods-and-properties"></a>TableAdapter 方法和属性  
 TableAdapter 类不是属于[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]。 这意味着你不能查找其文档中或**对象浏览器**。 在设计时，当你使用前面所述的向导之一创建。 在创建时分配到 TableAdapter 的名称基于你正在使用的表的名称。 例如，当创建基于一个名为数据库中的表的 TableAdapter `Orders`，名为 TableAdapter `OrdersTableAdapter`。 可以使用更改类名称的 TableAdapter**名称**属性中的**数据集设计器**。  
  
 以下是常用的方法和 Tableadapter 的属性：  
  
|成员|描述|  
|------------|-----------------|  
|`TableAdapter.Fill`|该表中填充 TableAdapter 的关联的数据的 TableAdapter 的 SELECT 命令的结果。|  
|`TableAdapter.Update`|将更改发送回数据库，并返回一个整数，表示更新影响的行数。 有关详细信息，请参阅[使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。|  
|`TableAdapter.GetData`|返回一个新<xref:System.Data.DataTable>使用数据进行填充。|  
|`TableAdapter.Insert`|在数据表中创建一个新行。 有关详细信息，请参阅[新记录插入数据库](../data-tools/insert-new-records-into-a-database.md)。|  
|`TableAdapter.ClearBeforeFill`|确定数据表之前调用其中一个将被清空`Fill`方法。|  
  
## <a name="tableadapter-update-method"></a>TableAdapter 更新方法  
 Tableadapter 使用数据命令来读取和写入数据库中。 TableAdapter 的初始`Fill`（主） 查询用于创建关联的数据的表的架构用作的基础，以及`InsertCommand`， `UpdateCommand`，和`DeleteCommand`与关联的命令`TableAdapter.Update`方法。 调用 TableAdapter`Update`方法运行语句时 TableAdapter 最初创建配置了，不是一个与已添加的其他查询**TableAdapter 查询配置向导**.  
  
 当使用 TableAdapter 时，它将有效地执行与你通常会执行的命令相同的操作。 例如，当调用该适配器`Fill`方法，该适配器运行数据命令其`SelectCommand`属性，并使用数据读取器 (例如， <xref:System.Data.SqlClient.SqlDataReader>) 要加载的结果集到数据表。 同样，当调用该适配器`Update`方法，它运行相应的命令 (在`UpdateCommand`， `InsertCommand`，和`DeleteCommand`属性) 为每个更改数据表中的记录。  
  
> [!NOTE]
> 如果没有足够的信息在主查询中， `InsertCommand`， `UpdateCommand`，和`DeleteCommand`生成 TableAdapter 时默认情况下创建命令。 如果 TableAdapter 的主查询不只是一个单表 SELECT 语句，就可以在设计器将无法生成`InsertCommand`， `UpdateCommand`，和`DeleteCommand`。 如果不会生成这些命令，在运行时，可能会收到错误`TableAdapter.Update`方法。  
  
## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter GenerateDbDirectMethods  
 除了`InsertCommand`， `UpdateCommand`，和`DeleteCommand`，可以直接对数据库运行的方法创建 Tableadapter。 这些方法 (`TableAdapter.Insert`， `TableAdapter.Update`，和`TableAdapter.Delete`) 可以调用直接以操作数据库中的数据。 这意味着您可以从您的代码而不是调用调用这些单个方法`TableAdapter.Update`处理插入、 更新和删除操作处于挂起状态的相关联的数据表。  
  
 如果不想要创建以下直接方法，设置 TableAdapter **GenerateDbDirectMethods**属性设置为`false`(在**属性**窗口)。 添加到 TableAdapter 的其他查询均为独立查询 — 它们不生成这些方法。  
  
## <a name="tableadapter-support-for-nullable-types"></a>TableAdapter 支持可以为 null 的类型  
 Tableadapter 支持可以为 null 的类型`Nullable(Of T)`和`T?`。 若要深入了解 Visual Basic 中可以为 null 的类型，请参阅[可以为 null 的值类型](https://msdn.microsoft.com/library/9ac3b602-6f96-4e6d-96f7-cd4e81c468a6)。 有关 C# 中可以为 null 类型的详细信息，请参阅[使用可以为 Null 的类型](https://msdn.microsoft.com/library/0bacbe72-ce15-4b14-83e1-9c14e6380c28)。  
  
## <a name="security"></a>安全性  
 当你使用数据命令时`CommandType`属性设置为<xref:System.Data.CommandType>，仔细检查并向其传递到数据库之前从客户端发送的信息。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 将内容传输到数据库的用户输入之前，始终验证信息有效。 一种最佳做法是始终使用参数化的查询或存储的过程在可能的情况。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
