---
title: 数据集工具
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vs.data.DataSet
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- untyped datasets
- datasets [Visual Basic], extended properties
- typed datasets
- current record in dataset
- XML [Visual Basic], datasets
- DataSet class, about datasets
- unique constraints (datasets)
- data relationships
- parent records in datasets
- extended properties, in typed datasets
- datasets [Visual Basic]
- schemas [Visual Basic], datasets
- datasets [Visual Basic], msprop
- master-detail tables, datasets
- databases [Visual Basic], updating
- msprop
- foreign keys, datasets
- DataSet class
- datasets [Visual Basic], filling
- case sensitivity, datasets
- constraints [Visual Basic], datasets
- child records
- related tables, datasets
- updating datasets, about dataset updates
- data caching, datasets
- DataRelation object, datasets
- untyped datasets, compared to typed datasets
- cache [Visual Studio], datasets
- datasets [Visual Basic], relationships
- related tables
- XML schemas, about XML schemas and datasets
- relationships, datasets
- typed datasets, compared to untyped datasets
- datasets [Visual Basic], populating
- datasets [Visual Basic], namespace
- data adapters, populating datasets
ms.assetid: ee57f4f6-9fe1-4e0a-be9a-955c486ff427
caps.latest.revision: 53
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 23e4deba53288383a569f6da6e14d27f723825ee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657388"
---
# <a name="dataset-tools-in-visual-studio"></a>Visual Studio 中的数据集工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 数据集和相关类是早期2000s 中的旧 .NET 技术，使应用程序可以在应用程序与数据库断开连接时使用内存中的数据。 它们对于允许用户修改数据并将更改保存回数据库的应用程序特别有用。 尽管数据集已证实成为一种非常成功的技术，但建议新的 .NET 应用程序使用实体框架。 实体框架提供了一种更自然的方式来处理作为对象模型的表格数据，并且它具有更简单的编程接口。

 数据集对象是一个实质上是小型数据库的内存中对象。 它包含 DataTable、DataColumn 和 DataRow 对象，您可以在其中存储和修改一个或多个数据库中的数据，而不必维护打开的连接。 数据集维护对其数据的更改的相关信息，以便在应用程序重新连接时，可以跟踪更新并将其发送回数据库。

 数据集和相关类在 .NET Framework 类库中的 System.web 命名空间中定义。 可以在代码中动态地创建和修改数据集。 有关如何执行此操作的详细信息，请参阅 ADO.NET。 本部分中的文档演示如何使用 Visual Studio 设计器处理数据集。 需要注意的一点是：通过设计器创建的数据集使用 TableAdapter 对象与数据库进行交互，而以编程方式使用 DataAdapter 对象进行数据集。 有关以编程方式创建数据集的信息，请参阅[dataadapter 和 datareader](https://msdn.microsoft.com/library/cc952ca2-ec19-46ab-9189-15174b52cb74)。

 如果你的应用程序只需要从数据库读取数据，而不执行更新、添加或删除操作，则通常可以通过使用 DataReader 对象将数据检索到泛型列表对象或其他集合对象来获得更好的性能。 如果要显示数据，可以将用户界面数据绑定到集合。

## <a name="dataset-workflow"></a>数据集工作流
 Visual Studio 提供了许多工具来简化数据集的使用。 基本的端到端工作流是：

- 使用 "**数据源**" 窗口，可以从一个或多个数据源创建新的数据集。 使用**数据集设计器**配置数据集并设置其属性。 例如，您需要指定要包含的数据源中的表以及每个表中的哪些列。 仔细选择以保留数据集所需的内存量。 有关详细信息，请参阅[创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)。

- 指定表之间的关系，以便正确处理外键。 有关详细信息，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

- 使用**TableAdapter 配置向导**指定将填充数据集的查询或存储过程，以及要实现的数据库操作（更新、删除等）。 有关详细信息，请参阅以下主题：

  - [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)

  - [编辑数据集中的数据](../data-tools/edit-data-in-datasets.md)

  - [验证数据集中的数据](../data-tools/validate-data-in-datasets.md)

  - [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)

- 查询并搜索数据集中的数据。 有关详细信息，请参阅[查询数据集](../data-tools/query-datasets.md)。 [!INCLUDE[linq_dataset](../includes/linq-dataset-md.md)] 对 <xref:System.Data.DataSet> 对象中的数据启用[LINQ （语言集成查询）](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) 。 有关详细信息，请参阅 [LINQ to DataSet](https://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17)。

- 使用 "**数据源**" 窗口可以将用户界面控件绑定到数据集或其单独的列，还可以指定哪些列是用户可编辑的列。 有关详细信息，请参阅[在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

## <a name="datasets-and-n-tier-architecture"></a>数据集和 N 层体系结构
 有关 N 层应用程序中的数据集的信息，请参阅[使用 n 层应用程序中的数据集](../data-tools/work-with-datasets-in-n-tier-applications.md)。

## <a name="datasets-and-xml"></a>数据集和 XML
 有关将数据集转换为 XML 或从 XML 转换数据集的信息，请参阅将[xml 数据读入数据集](../data-tools/read-xml-data-into-a-dataset.md)和[将数据集另存为 xml](../data-tools/save-a-dataset-as-xml.md)。

## <a name="see-also"></a>请参阅
 [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
