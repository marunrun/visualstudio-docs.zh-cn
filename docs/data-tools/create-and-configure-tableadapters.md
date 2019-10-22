---
title: 创建和配置 TableAdapter
ms.date: 09/01/2017
ms.topic: conceptual
helpviewer_keywords:
- table adapters, creating
- creating TableAdapters
- data [Visual Studio], creating data components
- data [Visual Studio], TableAdapters
- data [Visual Studio], creating table adapters
ms.assetid: 08630d69-0d6c-4e8f-b42d-2922f45f8415
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: f1403d61dd7a0d36401e449806fdafa6adc533b5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648603"
---
# <a name="create-and-configure-tableadapters"></a>创建和配置 TableAdapter

Tableadapter 提供应用程序和数据库之间的通信。 它们连接到数据库，运行查询或存储过程，并返回新的数据表或使用返回的数据填充现有 <xref:System.Data.DataTable>。 Tableadapter 还可以将更新后的数据从应用程序发送回数据库。

当你执行以下操作之一时，将为你创建 Tableadapter：

- 将数据库对象从**服务器资源管理器**拖动到**数据集设计器**中。

- 运行 "数据源配置向导"，并选择 "**数据库**" 或 " **Web 服务**" 数据源类型。

   ![Visual Studio 中的数据源配置向导](media/data-source-configuration-wizard.png)

你还可以创建新的 TableAdapter，并使用数据源对其进行配置，方法是将 TableAdapter 从**工具箱**拖动到**数据集设计器**图面中的空区域。

有关 Tableadapter 的简介，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="use-the-tableadapter-configuration-wizard"></a>使用 TableAdapter 配置向导

运行**TableAdapter 配置向导**来创建或编辑 tableadapter 及其关联的数据表。 您可以通过在**数据集设计器**中右键单击现有的 TableAdapter 来配置它。

![raddata 表适配器配置向导](../data-tools/media/raddata-table-adapter-configuration-wizard.png)

如果焦点位于**数据集设计器**上时从工具箱拖动新的 TableAdapter，向导将启动并提示您指定 TableAdapter 应连接到的数据源。 在下一页上，向导会询问它应该使用哪种类型的命令与数据库进行通信（SQL 语句或存储过程）。 （如果要配置的 TableAdapter 已与数据源关联，则不会看到此情况。）

- 如果对数据库具有正确的权限，则可以选择在基础数据库中创建新的存储过程。 如果没有这些权限，则无法选择此选项。

- 你还可以选择为 TableAdapter 的**SELECT**、 **INSERT**、 **UPDATE**和**DELETE**命令运行现有的存储过程。 例如，当调用 `TableAdapter.Update()` 方法时，将运行分配给**Update**命令的存储过程。

将参数从选中的存储过程映射到数据表中相应的列。 例如，如果您的存储过程接受一个名为 `@CompanyName` 的参数，该参数传递到表中的 `CompanyName` 列，则将 `@CompanyName` 参数的**源列**设置为 `CompanyName`。

> [!NOTE]
> 分配给 "SELECT" 命令的存储过程是通过调用在向导的下一步骤中命名的 TableAdapter 的方法来运行的。 默认方法是 `Fill`，因此，通常用于运行 SELECT 过程的代码是 `TableAdapter.Fill(tableName)` 的。 如果更改 `Fill` 的默认名称，请将 `Fill` 替换为指定的名称，并将 "TableAdapter" 替换为 TableAdapter 的实际名称（例如，`CustomersTableAdapter`）。

- 选择 "**创建将更新直接发送到数据库"** 选项的方法等效于将 `GenerateDBDirectMethods` 属性设置为 true。 当原始 SQL 语句未提供足够的信息或查询不是可更新的查询时，此选项不可用。 例如，**联接**查询和返回单个（标量）值的查询中可能会发生这种情况。

使用向导中的**高级选项**，您可以：

- 基于在 "**生成 SQL 语句**" 页上定义的 SELECT 语句生成 INSERT、UPDATE 和 DELETE 语句
- 使用开放式并发
- 指定是否在运行 INSERT 和 UPDATE 语句后刷新数据表

## <a name="configure-a-tableadapters-fill-method"></a>配置 TableAdapter 的 Fill 方法

有时，你可能需要更改 TableAdapter 的表的架构。 为此，请修改 TableAdapter 的主要 `Fill` 方法。 Tableadapter 是使用主要 `Fill` 方法创建的，该方法定义关联数据表的架构。 主 `Fill` 方法基于最初配置 TableAdapter 时输入的查询或存储过程。 它是数据集设计器中的数据表下的第一个（最顶层）方法。

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

对 TableAdapter 的 main `Fill` 方法所做的任何更改都会反映在关联数据表的架构中。 例如，从 main `Fill` 方法中的查询删除列还会从关联的数据表中删除列。 此外，从 main `Fill` 方法中删除列将从该 TableAdapter 的任何附加查询中删除该列。

您可以使用 TableAdapter 查询配置向导来创建和编辑用于 TableAdapter 的附加查询。 这些附加查询必须符合表架构，除非它们返回标量值。  每个附加查询都具有您指定的名称。

下面的示例演示了如何调用名为 `FillByCity` 的附加查询：

`CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")`

### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>使用新查询启动 TableAdapter 查询配置向导

1. 在“数据集设计器”中打开数据集。

2. 如果要创建新查询，请将 "**查询**" 对象从 "**工具箱**" 的 "**数据集**" 选项卡拖动到 <xref:System.Data.DataTable> 上，或从 TableAdapter 的快捷菜单中选择 "**添加查询**"。 您还可以将**查询**对象拖动到**数据集设计器**的空白区域，这将创建一个不带关联 <xref:System.Data.DataTable> 的 TableAdapter。 这些查询只能返回单个（标量）值，或对数据库运行 UPDATE、INSERT 或 DELETE 命令。

3. 在 "**选择你的数据连接**" 屏幕上，选择或创建查询将使用的连接。

    > [!NOTE]
    > 此屏幕仅在设计器无法确定要使用的正确连接时，或在没有可用连接时出现。

4. 在 "**选择命令类型**" 屏幕上，从数据库中提取数据的以下方法中进行选择：

    - **使用 sql 语句**可以键入 SQL 语句，以从数据库中选择数据。

    - "**创建新存储过程**" 使您能够使向导根据指定的 SELECT 语句创建新的存储过程（在数据库中）。

    - **使用现有的存储过程**可以在运行查询时运行现有的存储过程。

### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>在现有查询上启动 TableAdapter 查询配置向导

- 如果要编辑现有的 TableAdapter 查询，请右键单击该查询，然后从快捷菜单中选择 "**配置**"。

    > [!NOTE]
    > 右键单击 TableAdapter 的主查询会重新配置 TableAdapter，并 <xref:System.Data.DataTable> 架构。 不过，在 TableAdapter 上右键单击其他查询时，仅配置所选查询。 **Tableadapter 配置向导**重新配置 TableAdapter 定义，而**Tableadapter 查询配置向导**仅重新配置所选查询。

### <a name="to-add-a-global-query-to-a-tableadapter"></a>将全局查询添加到 TableAdapter

- 全局查询是返回单个（标量）值或没有值的 SQL 查询。 通常，全局函数执行数据库操作，例如插入、更新和删除。 它们还聚合信息，例如表中客户的计数或按特定顺序排列的所有项的总费用。

     您可以通过将**查询**对象从 "**工具箱**" 的 "**数据集**" 选项卡拖到**数据集设计器**的空白区域来添加全局查询。

- 提供执行所需任务的查询，例如 `SELECT COUNT(*) AS CustomerCount FROM Customers`。

    > [!NOTE]
    > 将**查询**对象直接拖到**数据集设计器**创建只返回标量（单个）值的方法。 尽管你选择的查询或存储过程可能会返回多个值，但向导创建的方法只返回单个值。 例如，查询可能返回返回的数据的第一行的第一列。

## <a name="see-also"></a>请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)