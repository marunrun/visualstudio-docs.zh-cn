---
title: 创建和配置数据集
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- typed datasets, creating
- datasets, creating
- datasets, configuring
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 41a7a699506853d6891c7d7b66fef4082814c06a
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65460621"
---
# <a name="how-to-create-and-configure-datasets-in-visual-studio"></a>如何：在 Visual Studio 中创建和配置数据集

数据集是一组对象在内存中存储数据库中的数据和支持更改跟踪来使创建、 读取、 更新和删除 (CRUD) 操作，对该数据而无需始终连接到数据库。 数据集设计用于简单*对数据的窗体*业务应用程序。 对于新应用程序，请考虑使用实体框架在内存中的数据存储和建模。 若要使用的数据集，应具有数据库概念的基础知识。

您可以创建类型化<xref:System.Data.DataSet>在设计时通过使用 Visual Studio 中的类**数据源配置向导**。 有关以编程方式创建数据集的信息，请参阅[创建数据集 (ADO.NET)](/dotnet/framework/data/adonet/dataset-datatable-dataview/creating-a-dataset)。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>使用数据源配置向导创建新的数据集

1. 在 Visual Studio 中，打开你的项目，然后选择**项目** > **添加新数据源**以启动**数据源配置向导**。

2. 选择要连接到的数据源的类型。

     ![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)

3. 选择将成为你的数据集的数据源的数据库。

     ![数据源选择的连接](../data-tools/media/data-source-choose-a-connection.png)

4. 选择表 （或单个列），存储过程、 函数和从你想要在数据集中表示数据库的视图。

     ![选择数据库对象](../data-tools/media/raddata-chose-objects.png)

5. 单击 **“完成”**。

   数据集显示为中的一个节点**解决方案资源管理器**。

   ![在解决方案资源管理器中的数据集](../data-tools/media/dataset-in-solution-explorer.png)

6. 单击中的数据集节点**解决方案资源管理器**以打开中的数据集**数据集设计器**。 在数据集中每个表都有一个关联`TableAdapter`对象，表示在底部。 表适配器用于填充数据集并根据需要将命令发送到数据库。

   ![数据集设计器](../data-tools/media/dataset-designer.png)

7. 连接这些表的关系行表示在数据库中定义的表之间的关系。 默认情况下，在数据库中的 foreign key 约束作为关系，表示与更新和删除规则设置为 none。 通常情况下，这是你想。 但是，可以单击这些线以显示**关系**对话框中，您可以在其中更改分层更新的行为。 有关详细信息，请参阅[中的数据集的关系](../data-tools/relationships-in-datasets.md)并[分层更新](../data-tools/hierarchical-update.md)。

     ![数据集关系对话框](../data-tools/media/raddata-relation-dialog.png)

8. 单击表、 表适配器或在表中的列名称以查看其属性在**属性**窗口。 您可以修改某些此处的值。 只需记住您正在修改数据集，不是源数据库。

     ![数据集列属性](../data-tools/media/dataset-column-properties.png)

9. 可以将新的表或表适配器添加到数据集，或添加现有的表适配器的新查询或指定新通过将这些项从表之间的关系**工具箱**选项卡。时，此选项卡会出现**数据集设计器**处于活动状态。

     ![数据集工具箱](../data-tools/media/raddata-dataset-toolbox.png)

接下来，你可能想要指定如何填充数据的数据集。 为此，请使用**TableAdapter 配置向导**。 有关详细信息，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>将数据库表或其他对象添加到现有数据集

此过程演示如何从用于首次创建数据集的相同数据库添加一个表。

1. 单击中的数据集节点**解决方案资源管理器**以便**数据集设计器**成为焦点。

2. 单击**数据源**Visual Studio 中或类型的左边距中的选项卡**数据源**在搜索框中。

3. 右键单击数据集节点，然后选择**使用向导配置数据源**。

     ![数据源上下文菜单](../data-tools/media/data-source-context-menu.png)

4. 使用向导来指定哪些其他表、 存储的过程或其他数据库对象添加到数据集。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>将独立的数据表添加到数据集

1. 在“数据集设计器”中打开数据集。

2. 拖动<xref:System.Data.DataTable>类派生**数据集**选项卡**工具箱**拖动到**数据集设计器**。

3. 添加列来定义您的数据的表。 右键单击该表，然后选择**外** > **列**。 使用**属性**窗口设置列和一个键的数据类型，如有必要。

独立的表需要实现`Fill`独立的表中的逻辑，以便可以填充数据。 有关填充独立的数据的表的信息，请参阅[填充数据集从 DataAdapter](/dotnet/framework/data/adonet/populating-a-dataset-from-a-dataadapter)。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [数据集中的关系](../data-tools/relationships-in-datasets.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)