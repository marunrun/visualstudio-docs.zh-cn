---
title: 使用 n 层应用程序中的数据集 |Microsoft Docs
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
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4f7be307ec94b15871da20ace8055fc7121d5d92
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657818"
---
# <a name="work-with-datasets-in-n-tier-applications"></a>在 n 层应用程序中使用数据集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

N 层数据应用程序 * 是以数据为中心的应用程序，分为多个逻辑层（或*层*）。 换句话说，N 层数据应用程序是分离到多个项目中的应用程序，数据访问层、业务逻辑层和表示层都在各自的项目中。 有关详细信息，请参阅[N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)。

 类型化数据集经过改进，现在可以在相互独立的项目中生成 TableAdapter 和数据集类。 这使你可以快速分离各应用程序层及生成 N 层数据应用程序。

 使用类型化数据集的 N 层支持，可以将应用程序体系结构迭代开发到 n 层设计。它还消除了将代码手动分隔到多个项目中的要求。 使用数据集设计器开始设计数据层。 如果已准备好对应用程序体系结构采用 n 层设计，请设置数据集的“数据集项目”属性，以在另一个项目中生成数据集类。

## <a name="in-this-section"></a>本节内容
 将[数据集和 Tableadapter 分隔到不同的项目中](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)描述如何将生成的数据集类从包含生成的 TableAdapter 类的项目中移出，并移到新项目中。

 [向 n 层应用程序中的 Tableadapter 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)介绍如何生成可在其中为 n 层 TableAdapter 添加代码的分部类。

 [将代码添加到 n 层应用程序中的数据集](../data-tools/add-code-to-datasets-in-n-tier-applications.md)介绍如何生成可在其中为 n 层数据集添加代码的分部类。

 [向 n 层数据集添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)描述在何处添加代码以对更改的数据执行验证。

 [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)提供用于创建类型化数据集以及将 TableAdapter 和数据集代码分离到多个项目中的分步说明。

 [演练：向 N 层数据应用程序添加验证](https://msdn.microsoft.com/library/b35d072c-31f0-49ba-a225-69177592c265)提供有关将验证添加到在 n 层数据应用程序演练中创建的应用程序的分步说明。

## <a name="reference"></a>参考
 <xref:System.Data.DataSet>

 <xref:System.Data.TypedTableBase%601>

## <a name="related-sections"></a>相关章节

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [使用 LINQ to SQL 的 N 层和远程应用程序](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)