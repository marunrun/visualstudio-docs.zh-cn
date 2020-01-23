---
title: 创建和配置数据集
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- typed datasets, creating
- datasets, creating
- datasets, configuring
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 8222b1985ab7f765be9b06fdd6abf7cb1e1cb2dc
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586908"
---
# <a name="how-to-create-and-configure-datasets-in-visual-studio"></a>如何：在 Visual Studio 中创建和配置数据集

数据集是一组对象，这些对象在内存中存储数据，并支持更改跟踪，以对这些数据启用创建、读取、更新和删除（CRUD）操作，而无需始终连接到数据库。 数据集专为数据业务应用程序的简单*窗体*而设计。 对于新应用程序，请考虑使用实体框架将数据存储在内存中并对其进行建模。 若要处理数据集，您应该具有数据库概念的基本知识。

您可以使用 "**数据源配置向导**" 在设计时在 Visual Studio 中创建类型化 <xref:System.Data.DataSet> 类。 有关以编程方式创建数据集的信息，请参阅[创建数据集（ADO.NET）](/dotnet/framework/data/adonet/dataset-datatable-dataview/creating-a-dataset)。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>使用 "数据源配置向导" 创建新数据集

1. 在 Visual Studio 中打开项目，然后选择 "**项目**" > "**添加新数据源**" 以启动 "**数据源配置向导**"。

2. 选择要连接的数据源的类型。

     ![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)

3. 选择将成为数据集的数据源的一个或哪些数据库。

     ![数据源选择连接](../data-tools/media/data-source-choose-a-connection.png)

4. 选择要在数据集中表示的数据库中的表（或单独的列）、存储过程、函数和视图。

     ![选择数据库对象](../data-tools/media/raddata-chose-objects.png)

5. 单击 **“完成”** 。

   数据集在**解决方案资源管理器**中显示为一个节点。

   ![解决方案资源管理器中的数据集](../data-tools/media/dataset-in-solution-explorer.png)

6. 单击**解决方案资源管理器**中的 "数据集" 节点，在 "**数据集设计器**" 中打开数据集。 数据集中的每个表都有一个关联的 `TableAdapter` 对象，它在底部表示。 表适配器用于填充数据集，并可选择将命令发送到数据库。

   ![数据集设计器](../data-tools/media/dataset-designer.png)

7. 连接表的关系线表示数据库中定义的表关系。 默认情况下，数据库中的外键约束仅表示为关系，更新和删除规则设置为 none。 通常，这是你想要的。 不过，您可以单击这些行以打开 "**关系**" 对话框，在其中可以更改分层更新的行为。 有关详细信息，请参阅数据集和[分层更新](../data-tools/hierarchical-update.md)[中的关系](../data-tools/relationships-in-datasets.md)。

     ![数据集关系对话框](../data-tools/media/raddata-relation-dialog.png)

8. 单击表中的表、表适配器或列名称可在 "**属性**" 窗口中查看其属性。 您可以在此处修改某些值。 请记住，你修改的是数据集，而不是源数据库。

     ![数据集列属性](../data-tools/media/dataset-column-properties.png)

9. 您可以向数据集添加新的表或表适配器，或添加现有表适配器的新查询，也可以通过从 "**工具箱**" 选项卡拖动这些项来指定表之间的新关系。当**数据集设计器**聚焦时，将显示此选项卡。

     ![数据集工具箱](../data-tools/media/raddata-dataset-toolbox.png)

接下来，你可能需要指定如何用数据填充数据集。 为此，请使用**TableAdapter 配置向导**。 有关详细信息，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>将数据库表或其他对象添加到现有数据集

此过程说明如何从用于首次创建数据集的同一数据库中添加表。

1. 单击**解决方案资源管理器**中的数据集节点，以将**数据集设计器**纳入焦点。

2. 单击 Visual Studio 左边距中的 "**数据源**" 选项卡，或在搜索框中键入 "**数据源**"。

3. 右键单击 "数据集" 节点，然后选择 "**用向导配置数据源**"。

     ![数据源上下文菜单](../data-tools/media/data-source-context-menu.png)

4. 使用该向导可以指定要添加到数据集的其他表、存储过程或其他数据库对象。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>向数据集添加独立数据表

1. 在“数据集设计器”中打开数据集。

2. 将 <xref:System.Data.DataTable> 类从 "**工具箱**" 的 "**数据集**" 选项卡拖到 "**数据集设计器**"。

3. 添加列以定义数据表。 右键单击该表，然后选择 "**添加** > **列**"。 如果需要，可以使用 "**属性**" 窗口设置列的数据类型和键。

独立表需要在独立的表中实现 `Fill` 逻辑，以便可以用数据填充它们。 有关填充独立数据表的信息，请参阅[从 DataAdapter 填充数据集](/dotnet/framework/data/adonet/populating-a-dataset-from-a-dataadapter)。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [数据集中的关系](../data-tools/relationships-in-datasets.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
