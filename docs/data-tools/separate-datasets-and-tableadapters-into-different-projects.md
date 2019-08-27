---
title: 将数据集和 TableAdapter 分离到不同的项目中
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: cb70705d29ad636329803656aeaa1a27ddf237d5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402766"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>将数据集和 TableAdapter 分离到不同的项目中
类型化数据集已得到增强，以便[Tableadapter](create-and-configure-tableadapters.md)和可以在不同的项目生成数据集类。 这使您可以快速分离各应用程序层及生成 n 层数据应用程序。

下面的过程介绍使用的过程**数据集设计器**以独立于包含生成的 TableAdapter 代码的项目的项目中生成数据集代码。

## <a name="separate-datasets-and-tableadapters"></a>单独的数据集和 Tableadapter
当与 TableAdapter 代码分离数据集的代码时，包含数据集代码的项目必须位于当前解决方案中。 如果此项目不在当前的解决方案，它不会在中可用**数据集项目**列表中**属性**窗口。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>若要将数据集划分为不同的项目

1. 打开包含数据集的解决方案 (*.xsd*文件)。

    > [!NOTE]
    > 如果解决方案不包含想要将数据集代码分离到其中的项目，创建项目，或将现有项目添加到解决方案。

2. 双击类型化数据集文件 ( *.xsd*文件) 中**解决方案资源管理器**以打开中的数据集**数据集设计器**。

3. 选择的空白区域**数据集设计器**。

4. 在中**属性**窗口中，找到**数据集项目**节点。

5. 在中**数据集项目**列表中，选择要在其中生成数据集代码的项目的名称。

     选择想要生成数据集代码中，在其中的项目后**数据集文件**属性填充默认的文件名。 如有必要，可以更改此名称。 此外，如果你想要为特定目录中生成数据集代码，则可以设置**项目文件夹**属性设置为的文件夹名称。

    > [!NOTE]
    > 当你将数据集和 Tableadapter (通过设置**数据集项目**属性)，将不会自动移动项目中的现有数据集分部类。 向数据集项目，必须手动移动现有数据集分部类。

6. 保存的数据集。

     数据集代码生成到中的选定项目**数据集项目**属性，并**TableAdapter**到当前项目生成代码。

默认情况下，单独的数据集和 TableAdapter 代码后结果将是每个项目中的离散类文件。 原始项目将包含名为的文件*DatasetName.Designer.vb* (或*DatasetName.Designer.cs*)，其中包含 TableAdapter 代码。 中指定的项目**数据集项目**属性具有名为的文件*DatasetName.DataSet.Designer.vb* (或*DatasetName.DataSet.Designer.cs*)，包含的数据集代码。

> [!NOTE]
> 若要查看生成的类文件，选择数据集的 TableAdapter 项目。 然后，在**解决方案资源管理器**，选择**显示所有文件**。

## <a name="see-also"></a>请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [演练：创建 n 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [ADO.NET](/dotnet/framework/data/adonet/index)