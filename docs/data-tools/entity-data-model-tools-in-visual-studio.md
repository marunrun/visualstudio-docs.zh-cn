---
title: 实体框架工具
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 53b87ce39f0eb5b1455f0a38b2aea7cc6b604342
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648531"
---
# <a name="entity-framework-tools-in-visual-studio"></a>Visual Studio 中的 Entity Framework Tools

实体框架是一种对象关系映射技术，它使 .NET 开发人员能够使用特定于域的对象处理关系数据。 它不要求提供开发人员通常需要编写的大部分数据访问代码。 对于新的 .NET 应用程序，实体框架是建议的对象关系映射（ORM）建模技术。

Entity Framework Tools 旨在帮助您生成实体框架（EF）应用程序。 实体框架的完整文档位于此处：[概述-EF 6](/ef/ef6/)。

  > [!NOTE]
  > 本页中所述的 Entity Framework Tools 用于生成 *.edmx*文件，这些文件在 EF Core 中不受支持。 若要从现有数据库生成 EF Core 模型，请参阅[反向工程-EF Core](/ef/core/managing-schemas/scaffolding)。 有关 EF 6 与 EF Core 之间的差异的详细信息，请参阅[比较 ef 6 和 EF Core](/ef/efcore-and-ef6/)。

使用 Entity Framework Tools，可以从现有数据库创建*概念模型*，然后以图形方式直观显示和编辑概念模型。 或者，您可以首先以图形方式创建概念模型，然后生成支持模型的数据库。 无论哪种情况，你都可以在基础数据库更改时自动更新模型，并为应用程序生成对象层代码。 数据库生成和对象层代码生成是可自定义的。

实体框架工具作为 Visual Studio 安装程序中的**数据存储和处理**工作负荷的一部分安装。 你还可以将它们作为单个组件安装在 " **sdk、库和框架**" 类别下。

这些是在 Visual Studio 中构成实体框架工具的特定工具：

- 您可以使用 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] 设计器**（**Entity Designer**）直观地创建和修改实体、关联、映射以及继承关系。 **Entity Designer**还会生成 [!INCLUDE[TLA#tla_cshrp](../data-tools/includes/tlasharptla_cshrp_md.md)] 或 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 的对象层代码。

- 您可以使用 **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] 向导**通过现有数据库生成概念模型，并将数据库连接信息添加到您的应用程序。

- 您可以使用 "**创建数据库向导**" 先创建概念模型，然后创建支持该模型的数据库。

- 在对基础数据库进行更改后，可以使用**模型更新向导**来更新概念模型、存储模型和映射。

  > [!NOTE]
  > 从 Visual Studio 2010 开始，实体框架工具不支持 [!INCLUDE[ss2k](../data-tools/includes/ss2k_md.md)]。

这些工具可生成或修改 *.edmx*文件。 此 *.edmx*文件包含描述概念模型、存储模型和这些模型之间的映射的信息。 有关详细信息，请参阅[EDMX](https://docs.microsoft.com/ef/ef6/)。

[实体框架 Power Tools](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EntityFrameworkPowerToolsBeta4)可帮助生成使用实体数据模型的应用程序。 Power tools 可以生成概念模型、验证现有模型、生成包含基于概念模型的对象类的源代码文件，并生成包含模型生成的视图的源代码文件。 有关详细信息，请参阅[预生成的映射视图](https://docs.microsoft.com/ef/ef6/fundamentals/performance/pre-generated-views)。

## <a name="related-topics"></a>相关主题

| Title | 描述 |
| - | - |
| [ADO.NET 实体框架](/dotnet/framework/data/adonet/ef/index) | 描述如何使用 [!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)] 提供的 [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] 工具来创建应用程序。 |
| [实体数据模型](/dotnet/framework/data/adonet/entity-data-model) | 提供有关使用 [!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)] 上构建的应用程序所使用的数据的链接和信息。 |
| [实体框架（EF）文档）](https://docs.microsoft.com/ef/ef6/get-started) | 提供视频、教程和高级文档的索引，以帮助您充分利用实体框架。 |
| [ASP.NET 5 应用程序到新数据库](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html) | 介绍如何使用实体框架7创建新的 ASP.NET 5 应用程序。 |

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)