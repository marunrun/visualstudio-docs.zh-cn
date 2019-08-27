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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6864708d3e60898b32ba07b14939a5c3e31d897e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705151"
---
# <a name="create-and-configure-datasets-in-visual-studio"></a>在 Visual Studio 中创建和配置数据集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

一个*数据集*是一组在内存中存储数据库中的数据和支持更改跟踪，若要启用的对象的创建、 读取、 更新和删除 (CRUD) 操作，对该数据而无需始终连接到数据库。 数据集设计用于简单*对数据的窗体*业务应用程序。 对于新应用程序，请考虑使用实体框架在内存中的数据存储和建模。 若要使用的数据集，应具有数据库概念的基础知识。

 创建类型化<xref:System.Data.DataSet>在设计时通过使用 Visual Studio 中的类**数据源配置向导**。 有关以编程方式创建数据集的信息，请参阅[创建数据集](https://msdn.microsoft.com/library/57629d8f-393e-4677-8b83-29ffde27f5fc)。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>使用数据源配置向导创建新的数据集

1. 上**项目**菜单上，单击**添加新数据源**以启动**数据源配置向导**。

2. 选择要连接到的数据源的类型。

     ![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png "数据源配置向导")

3. 对于数据库，选择将成为你的数据集的数据源的数据库。

     ![数据源选择的连接](../data-tools/media/data-source-choose-a-connection.png "数据源选择的连接")

4. 选择表 （或单个列），存储过程、 函数和从你想要在数据集中表示数据库的视图。

     ![选择数据库对象](../data-tools/media/raddata-chose-objects.png "raddata 选择对象")

5. 单击 **“完成”**。

6. 数据集显示为中的一个节点**解决方案资源管理器**:

     ![在解决方案资源管理器中的数据集](../data-tools/media/dataset-in-solution-explorer.png "在解决方案资源管理器中的数据集")

     单击该节点，然后在显示该数据集**数据集设计器**。 请注意，每个表中数据集关联的 TableAdapter 对象，表示在底部。 表适配器用于填充数据集并根据需要将命令发送到数据库。

     ![数据集设计器](../data-tools/media/dataset-designer.png "数据集设计器")

7. 连接这些表的关系行表示在数据库中定义的表之间的关系。 默认情况下，在数据库中的 foreign key 约束作为关系，表示与更新和删除规则设置为 none。 通常情况下，这是你想。 但是，可以单击这些线以显示**关系**对话框中，您可以在其中更改分层更新的行为。 有关详细信息，请参阅[中的数据集的关系](../data-tools/relationships-in-datasets.md)并[分层更新](../data-tools/hierarchical-update.md)。

     ![数据集关系对话框](../data-tools/media/raddata-relation-dialog.png "raddata 关系对话框")

8. 单击表、 表适配器或在表中的列名称以查看其属性在**属性**窗口。 您可以修改某些此处的值。 只需记住您正在修改数据集，不是源数据库。

     ![数据集列属性](../data-tools/media/dataset-column-properties.png "数据集列属性")

9. 可以将新的表或表适配器添加到数据集，或添加现有的表适配器的新查询或指定新通过将这些项从表之间的关系**工具箱**选项卡。时，此选项卡会出现**数据集设计器**处于活动状态。

     ![数据集工具箱](../data-tools/media/raddata-dataset-toolbox.png "raddata 数据集工具箱")

10. 接下来，您可能需要指定如何填充数据的数据集。 为此，请使用**TableAdapter 配置向导**。 有关详细信息，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>将数据库表或其他对象添加到现有数据集
 此过程演示如何从用于首次创建数据集的相同数据库添加一个表。

1. 单击中的数据集节点**解决方案资源管理器**使数据集设计器成为焦点。

2. 单击**数据源**选项卡中的 Visual Studio 中，左边距或输入`Data Sources`中**快速启动**。

3. 右键单击数据集节点，然后选择**使用向导配置数据源**。

     ![数据源上下文菜单](../data-tools/media/data-source-context-menu.png "数据源的上下文菜单")

4. 使用向导来指定哪些其他表或存储的过程或其他数据库对象，将添加到数据集。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>将独立的数据表添加到数据集

1. 在“数据集设计器”中打开数据集。

2. 拖动<xref:System.Data.DataTable>类派生**数据集**选项卡**工具箱**拖动到**数据集设计器**。

3. 添加列来定义您的数据的表。 有关详细信息，请参阅[如何：向数据表添加列](https://msdn.microsoft.com/library/8ca21f77-b99a-47a7-a656-7cfd7a1bd9df)。

4. 独立的表需要实现`Fill`独立的表中的逻辑，以便可以填充数据。 有关填充独立的数据的表的信息，请参阅[填充数据集从 DataAdapter](https://msdn.microsoft.com/library/3fa0ac7d-e266-4954-bfac-3fbe2f913153)。
