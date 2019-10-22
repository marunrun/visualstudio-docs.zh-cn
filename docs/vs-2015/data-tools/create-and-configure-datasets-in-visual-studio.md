---
title: 创建和配置数据集
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
- typed datasets, creating
- datasets [Visual Basic], creating
ms.assetid: 58f33b43-24e1-43b1-b08b-b74329960bd6
caps.latest.revision: 39
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3c84105387c708fa16e0b1d5c3294ef909466524
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72631196"
---
# <a name="create-and-configure-datasets-in-visual-studio"></a>在 Visual Studio 中创建和配置数据集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*数据集*是一组对象，这些对象在内存中存储数据，并支持更改跟踪，以对这些数据启用创建、读取、更新和删除（CRUD）操作，而无需始终连接到数据库。 数据集专为数据业务应用程序的简单*窗体*而设计。 对于新应用程序，请考虑使用实体框架将数据存储在内存中并对其进行建模。 若要处理数据集，您应该具有数据库概念的基本知识。

 您可以使用 "**数据源配置向导**" 在设计时在 Visual Studio 中创建类型化 <xref:System.Data.DataSet> 类。 有关以编程方式创建数据集的信息，请参阅[创建数据集](https://msdn.microsoft.com/library/57629d8f-393e-4677-8b83-29ffde27f5fc)。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>使用 "数据源配置向导" 创建新数据集

1. 在 "**项目**" 菜单上，单击 "**添加新数据源**" 以启动 "**数据源配置向导**"。

2. 选择要连接到的数据源的类型。

     ![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png "数据源配置向导")

3. 对于 "数据库"，请选择将成为数据集的数据源的一个或哪些数据库。

     ![数据源选择连接](../data-tools/media/data-source-choose-a-connection.png "数据源选择连接")

4. 选择要在数据集中表示的数据库中的表（或单独的列）、存储过程、函数和视图。

     ![选择数据库对象](../data-tools/media/raddata-chose-objects.png "raddata 选择的对象")

5. 单击 **“完成”** 。

6. 数据集在**解决方案资源管理器**中显示为一个节点：

     ![解决方案资源管理器中的数据集](../data-tools/media/dataset-in-solution-explorer.png "解决方案资源管理器中的数据集")

     单击该节点，数据集将出现在**数据集设计器**中。 请注意，数据集中的每个表都有一个关联的 TableAdapter 对象，它在底部表示。 表适配器用于填充数据集，并可选择将命令发送到数据库。

     ![数据集设计器](../data-tools/media/dataset-designer.png "数据集设计器")

7. 连接表的关系线表示数据库中定义的表关系。 默认情况下，数据库中的外键约束仅表示为关系，更新和删除规则设置为 none。 通常，这是你想要的。 不过，您可以单击这些行以打开 "**关系**" 对话框，在其中可以更改分层更新的行为。 有关详细信息，请参阅数据集和[分层更新](../data-tools/hierarchical-update.md)[中的关系](../data-tools/relationships-in-datasets.md)。

     ![数据集关系对话框](../data-tools/media/raddata-relation-dialog.png "raddata 关系对话框")

8. 单击表中的表、表适配器或列名称可在 "**属性**" 窗口中查看其属性。 您可以在此处修改某些值。 请记住，你修改的是数据集，而不是源数据库。

     ![数据集列属性](../data-tools/media/dataset-column-properties.png "数据集列属性")

9. 您可以向数据集添加新的表或表适配器，或添加现有表适配器的新查询，也可以通过从 "**工具箱**" 选项卡拖动这些项来指定表之间的新关系。当**数据集设计器**聚焦时，将显示此选项卡。

     ![数据集工具箱](../data-tools/media/raddata-dataset-toolbox.png "raddata 数据集工具箱")

10. 接下来，你可能需要指定如何用数据填充数据集。 为此，请使用**TableAdapter 配置向导**。 有关详细信息，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>将数据库表或其他对象添加到现有数据集
 此过程说明如何从用于首次创建数据集的同一数据库中添加表。

1. 单击**解决方案资源管理器**中的数据集节点，以将数据集设计器纳入焦点。

2. 单击 Visual Studio 左边距中的 "**数据源**" 选项卡，或在**快速启动**栏中输入 `Data Sources`。

3. 右键单击 "数据集" 节点，然后选择 "**用向导配置数据源**"。

     ![数据源上下文菜单](../data-tools/media/data-source-context-menu.png "数据源上下文菜单")

4. 使用该向导可以指定要添加到数据集的其他表或存储过程或其他数据库对象。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>向数据集添加独立数据表

1. 在“数据集设计器”中打开数据集。

2. 将 <xref:System.Data.DataTable> 类从 "**工具箱**" 的 "**数据集**" 选项卡拖到 "**数据集设计器**"。

3. 添加列以定义数据表。 有关详细信息，请参阅[如何：将列添加到 DataTable](https://msdn.microsoft.com/library/8ca21f77-b99a-47a7-a656-7cfd7a1bd9df)。

4. 独立表需要在独立的表中实现 `Fill` 逻辑，以便可以用数据填充它们。 有关填充独立数据表的信息，请参阅[从 DataAdapter 填充数据集](https://msdn.microsoft.com/library/3fa0ac7d-e266-4954-bfac-3fbe2f913153)。
