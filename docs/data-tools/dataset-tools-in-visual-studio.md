---
title: 数据集工具
ms.date: 11/21/2018
ms.topic: conceptual
f1_keywords:
- vs.data.DataSet
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ead32426585ecd4962ccc869f470021c5d0976fe
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821371"
---
# <a name="dataset-tools-in-visual-studio"></a>Visual Studio 中的数据集工具

> [!NOTE]
> 数据集和相关的类是从年初，使应用程序的应用程序从数据库断开连接时，可以使用在内存中数据的旧.NET 技术。 它们是特别有用的应用程序使用户能够修改数据和持久保存回数据库的更改。 尽管数据集已证明是非常成功的技术，我们建议新的.NET 应用程序使用 Entity Framework。 实体框架提供更简单的方式来使用表格格式数据作为对象模型，它具有一个更简单的编程接口。

一个`DataSet`对象是一个内存中对象，它实质上是一个最小化数据库。 它包含`DataTable`， `DataColumn`，和`DataRow`对象可以用于存储和修改一个或多个数据库中的数据，而无需维护的开放连接。 数据集维护对其数据的更改的信息，因此可以跟踪更新和应用程序变得重新连接时发送回数据库。

数据集和相关的类定义中<xref:System.Data?displayProperty=fullName>.NET API 中的命名空间。 可以创建和修改动态地在代码中使用 ADO.NET 数据集。 在本部分中的文档演示如何通过使用 Visual Studio 设计器处理数据集。 创建通过设计器使用的数据集**TableAdapter**对象与数据库进行交互。 以编程方式创建的数据集使用**DataAdapter**对象。 有关以编程方式创建数据集的信息，请参阅[Dataadapter 和 Datareader](/dotnet/framework/data/adonet/dataadapters-and-datareaders)。

如果你的应用程序需要仅从数据库读取数据并不执行更新、 添加，或删除，通常可以通过获取更好的性能`DataReader`对象将数据检索到一个泛型`List`对象或另一个集合对象。 如果要显示数据，您可以对数据绑定的用户界面集合。

## <a name="dataset-workflow"></a>数据集的工作流

Visual Studio 提供了工具，简化数据集的处理。 基本的端到端工作流是：

- 使用[数据源窗口](add-new-data-sources.md#data-sources-window)从一个或多个数据源创建新的数据集。 使用**数据集设计器**配置数据集并设置其属性。 例如，您需要指定哪些数据源包括，从表和每个表中的哪些列。 请仔细选择以节省数据集需要的内存量。 有关详细信息，请参阅[创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)。

- 指定表之间的关系，以便正确处理外键。 有关详细信息，请参阅[使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

- 使用**TableAdapter 配置向导**指定的查询或存储的过程填充数据集，并实现哪些数据库操作 （update、 delete 等）。 有关详细信息，请参阅以下主题：

  - [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)

  - [编辑数据集中的数据](../data-tools/edit-data-in-datasets.md)

  - [验证数据集中的数据](../data-tools/validate-data-in-datasets.md)

  - [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)

- 查询并在数据集中搜索的数据。 有关详细信息，请参阅[查询数据集](../data-tools/query-datasets.md)。 [!INCLUDE[linq_dataset](../data-tools/includes/linq_dataset_md.md)] 使[LINQ （语言集成查询）](/dotnet/csharp/linq/)中的数据通过<xref:System.Data.DataSet>对象。 有关详细信息，请参阅 [LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)。

- 使用**数据源**窗口来将用户界面控件绑定到的数据集或其单独的列，并指定哪些列是用户可编辑。 有关详细信息，请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

## <a name="datasets-and-n-tier-architecture"></a>数据集和 N 层体系结构

有关 N 层应用程序中的数据集的信息，请参阅[使用 n 层应用程序中的数据集](../data-tools/work-with-datasets-in-n-tier-applications.md)。

## <a name="datasets-and-xml"></a>数据集和 XML

有关转换以及从 XML 转换为数据集的信息，请参阅[读取 XML 数据读入数据集](../data-tools/read-xml-data-into-a-dataset.md)并[将数据集另存为 XML](../data-tools/save-a-dataset-as-xml.md)。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
