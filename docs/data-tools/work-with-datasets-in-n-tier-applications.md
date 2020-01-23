---
title: 在 n 层应用程序中使用数据集
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- datasets [Visual Basic], n-tier applications
- multi-tier database applications
- DataSet project [VS n-tier applications]
- distributed applications [VS n-tier applications]
- data [Visual Basic], n-tier applications
- TableAdapters, n-tier applications
- n-tier applications
- tiers, n-tier applications
- typed datasets, n-tier applications
- multiple tier applications
ms.assetid: f6ae2ee0-ea5f-4a79-8f4b-e21c115afb20
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: c7532bed6a7d43c24d698870723d2265fc2b176f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585920"
---
# <a name="work-with-datasets-in-n-tier-applications"></a>在 n 层应用程序中使用数据集

“N 层数据应用程序”是以数据为中心且分为多个逻辑层（或“多层”）的应用程序。 换句话说，N 层数据应用程序是分离到多个项目中的应用程序，数据访问层、业务逻辑层和表示层都在各自的项目中。 有关详细信息，请参阅[N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)。

类型化数据集经过改进，现在可以在相互独立的项目中生成 TableAdapter 和数据集类。 这使你可以快速分离各应用程序层及生成 N 层数据应用程序。

使用类型化数据集的 N 层支持，可以将应用程序体系结构迭代开发到 n 层设计。它还消除了将代码手动分隔到多个项目中的要求。 使用**数据集设计器**开始设计数据层。 如果已准备好对应用程序体系结构采用 n 层设计，请设置数据集的“数据集项目”属性，以在另一个项目中生成数据集类。

## <a name="reference"></a>引用

- <xref:System.Data.DataSet>
- <xref:System.Data.TypedTableBase%601>

## <a name="see-also"></a>另请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [演练：创建 n 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [向 N 层应用程序中的 TableAdapter 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [向 N 层应用程序的数据集添加代码](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [向 N 层数据集添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)
- [将数据集和 TableAdapter 分离到不同的项目中](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [创建和配置 Tableadapter](../data-tools/create-and-configure-tableadapters.md)
- [使用 LINQ to SQL 的 n 层和远程应用程序](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)
