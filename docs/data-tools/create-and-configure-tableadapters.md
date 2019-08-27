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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 026b670deb5beff42c927894ee9851ddb3ccc3ad
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62567517"
---
# <a name="create-and-configure-tableadapters"></a>创建和配置 TableAdapter

Tableadapter 提供你的应用程序和数据库之间的通信。 在连接到数据库、 运行的查询或存储的过程，并返回新的数据的表或填充现有<xref:System.Data.DataTable>返回的数据。 Tableadapter 还可以从你的应用程序与数据库发送更新后的数据。

当您执行以下操作之一时，会为您创建 Tableadapter:

- 将从数据库对象拖放**服务器资源管理器**成**数据集设计器**。

- 运行数据源配置向导，并选择**数据库**或**Web 服务**数据源类型。

   ![在 Visual Studio 中的数据源配置向导](media/data-source-configuration-wizard.png)

此外可以创建新的 TableAdapter，并将其配置与数据源中，通过拖动从 TableAdapter**工具箱**到空区域中**数据集设计器**图面。

Tableadapter 的简介，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="use-the-tableadapter-configuration-wizard"></a>使用 TableAdapter 配置向导

运行**TableAdapter 配置向导**若要创建或编辑 Tableadapter 及其关联的 Datatable。 可以通过右键单击在其上配置现有 TableAdapter**数据集设计器**。

![raddata 表适配器配置向导](../data-tools/media/raddata-table-adapter-configuration-wizard.png)

如果从工具箱拖动新的 TableAdapter 时**数据集设计器**焦点，向导将启动并提示您指定的数据源 TableAdapter 应连接到处于。 在下一页上，向导会要求它应使用哪种类型的命令与 SQL 语句或存储的过程的数据库进行通信。 （您看不到此如果您在配置 TableAdapter 已与数据源相关联。）

- 您可以选择基础数据库中创建新的存储的过程，如果您具有正确的权限的数据库。 如果没有这些权限，这不会作为一个选项。

- 您还可以选择运行的现有存储的过程**选择**，**插入**，**更新**，以及**删除**的命令TableAdapter。 分配给该存储的过程**更新**命令，例如，运行时`TableAdapter.Update()`调用方法。

将参数从选中的存储过程映射到数据表中相应的列。 例如，如果你的存储的过程接受一个名为参数`@CompanyName`它传递给`CompanyName`在表中，列集**源列**的`@CompanyName`参数`CompanyName`。

> [!NOTE]
> 分配给 SELECT 命令的存储的过程是通过调用 TableAdapter 的方法，命名该向导的下一步中运行。 默认方法是`Fill`，因此通常用来运行 SELECT 过程的代码是`TableAdapter.Fill(tableName)`。 如果更改中的默认名称`Fill`，将替换`Fill`名称分配和"TableAdapter"替换为 TableAdapter 的实际名称 (例如， `CustomersTableAdapter`)。

- 选择**创建方法以将更新发送到数据库直接**选项等同于设置`GenerateDBDirectMethods`属性设为 true。 当原始 SQL 语句未提供足够的信息或查询不是可更新的查询时，此选项不可用。 发生此情况，例如，在**加入**查询和返回单个 （标量） 值的查询。

**高级选项**向导中，您可以：

- 生成基于定义的 SELECT 语句的 INSERT、 UPDATE 和 DELETE 语句**生成 SQL 语句**页
- 使用开放式并发
- 指定是否在插入后刷新数据的表和运行 UPDATE 语句

## <a name="configure-a-tableadapters-fill-method"></a>配置 TableAdapter 的 Fill 方法

有时你可能想要更改 TableAdapter 的表的架构。 若要执行此操作，您可以修改 TableAdapter 的主`Fill`方法。 使用主键创建 Tableadapter`Fill`方法，用于定义关联的数据的表的架构。 主`Fill`方法基于查询或在最初配置 TableAdapter 时输入的存储的过程。 它是数据集设计器中的数据表的第一个 （最顶部） 方法。

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

向 TableAdapter 所做的任何更改的主`Fill`方法将反映在关联的数据的表的架构中。 例如，从主查询中删除列`Fill`方法将同时删除关联的数据表格中的列。 此外，从 main 中删除该列`Fill`方法移除列从任何其他查询的 TableAdapter。

TableAdapter 查询配置向导可用于创建和编辑其他查询的 TableAdapter。 这些附加的查询必须符合表架构，除非它们返回一个标量值。  每个其他查询具有你指定的名称。

下面的示例演示如何调用名为一个额外查询`FillByCity`:

`CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")`

### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>若要开始使用新查询的 TableAdapter 查询配置向导

1. 在“数据集设计器”中打开数据集。

2. 如果要创建一个新的查询，请拖动**查询**对象从**数据集**选项卡**工具箱**拖到<xref:System.Data.DataTable>，或选择**添加查询**TableAdapter 的快捷菜单中。 您还可以拖动**查询**对象拖放到的空白区域**数据集设计器**，这将创建没有关联的 TableAdapter <xref:System.Data.DataTable>。 这些查询可以只返回单个 （标量） 值或运行的 UPDATE、 INSERT 或删除对数据库的命令。

3. 上**选择数据连接**屏幕上，选择或创建该查询要使用的连接。

    > [!NOTE]
    > 当在设计器无法确定正确的连接，若要使用，或没有连接可用时，才会显示此屏幕。

4. 上**选择命令类型**屏幕上，从以下方法从数据库提取数据的选择：

    - **使用 SQL 语句**使您可以键入 SQL 语句，以从您的数据库选择的数据。

    - **创建新的存储的过程**使你能够在该向导创建新存储过程 （在数据库中） 根据指定的 SELECT 语句。

    - **使用现有存储的过程**，可运行查询时运行现有的存储的过程。

### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>若要启动 TableAdapter 查询配置向导在现有的查询

- 如果正在编辑现有 TableAdapter 查询，该查询中，右键单击，然后选择**配置**从快捷菜单。

    > [!NOTE]
    > 右键单击 TableAdapter 的主查询重新配置 TableAdapter 和<xref:System.Data.DataTable>架构。 右键单击 TableAdapter 上的其他查询，但是，配置所选的查询。 **TableAdapter 配置向导**重新配置 TableAdapter 定义，而**TableAdapter 查询配置向导**重新配置所选的查询。

### <a name="to-add-a-global-query-to-a-tableadapter"></a>若要向 TableAdapter 添加全局查询

- 全局查询是 SQL 查询返回单个 （标量） 值或空值。 通常情况下，全局函数执行数据库操作如插入、 更新和删除。 它们还聚合信息，如表或特定的顺序中的所有项的总费用的客户的计数。

     通过拖动添加全局查询**查询**对象从**数据集**选项卡**工具箱**拖到空区域中**数据集设计器**.

- 提供查询，例如，执行所需的任务， `SELECT COUNT(*) AS CustomerCount FROM Customers`。

    > [!NOTE]
    > 拖动**查询**直接拖到对象**数据集设计器**创建返回标量 （单个） 值的方法。 虽然查询或您选择的存储的过程可能返回多个单个值，由向导创建的方法仅返回单个值。 例如，查询可能返回返回的数据的第一行的第一列。

## <a name="see-also"></a>请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)