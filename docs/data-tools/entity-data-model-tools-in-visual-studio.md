---
title: 实体框架工具
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: eace6e7f3d970de5aa0ab0e74530d3182af0e177
ms.sourcegitcommit: 16d8ffc624adb716753412a22d586eae68a29ba2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412288"
---
# <a name="entity-framework-tools-in-visual-studio"></a>在 Visual Studio 中的实体框架工具

Entity Framework 是一种对象关系映射技术，使.NET 开发人员能够通过使用特定于域的对象处理关系数据。 它不要求提供开发人员通常需要编写的大部分数据访问代码。 实体框架是建模技术，用于新的.NET 应用程序的建议的对象关系映射 (ORM)。

实体框架工具旨在帮助你构建 Entity Framework (EF) 应用程序。 此处是有关实体框架的完整文档：[概述-EF 6](/ef/ef6/)。

  > [!NOTE]
  > 在此页上所述的实体框架工具用于生成 *.edmx*在 EF Core 中不支持的文件。 若要从现有数据库生成的 EF Core 模型，请参阅[反向工程-EF Core](/ef/core/managing-schemas/scaffolding)。 EF 6 和 EF Core 之间的差异的详细信息，请参阅[比较 EF 6 和 EF Core](/ef/efcore-and-ef6/)。

使用 Entity Framework Tools，您可以创建*概念模型*从现有数据库，然后以图形方式直观显示和编辑概念模型。 或者，您可以首先以图形方式创建概念模型，然后生成支持模型的数据库。 无论哪种情况，你都可以在基础数据库更改时自动更新模型，并为应用程序生成对象层代码。 数据库生成和对象层代码生成是可自定义的。

实体框架工具安装的一部分**数据存储和处理**Visual Studio 安装程序中的工作负荷。 您还可以作为单个组件下安装它们**Sdk、 库和框架**类别。

这些是组成 Visual Studio 中的实体框架工具的特定工具：

- 可以使用[!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)]  **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)]设计器**(**实体设计器**) 直观地创建和修改实体、 关联、 映射和继承关系。 **实体设计器**还会生成[!INCLUDE[TLA#tla_cshrp](../data-tools/includes/tlasharptla_cshrp_md.md)]或[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]对象层代码。

- 可以使用 **[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)]向导**从现有数据库生成概念模型并将数据库连接信息添加到你的应用程序。

- 可以使用**创建数据库向导**首先创建概念模型，然后创建支持该模型的数据库。

- 可以使用**模型更新向导**基础数据库发生更改时，更新概念模型、 存储模型和映射。

  > [!NOTE]
  > 从 Visual Studio 2010 开始，不支持实体框架工具[!INCLUDE[ss2k](../data-tools/includes/ss2k_md.md)]。

这些工具生成或修改 *.edmx*文件。 这 *.edmx*文件包含描述概念模型、 存储模型中，以及它们之间的映射信息。 有关详细信息，请参阅[EDMX](https://docs.microsoft.com/ef/ef6/)。

[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EntityFrameworkPowerToolsBeta4)帮助您生成使用实体数据模型的应用程序。 增强工具可以生成概念模型、 验证现有模型、 生成包含基于概念模型中，对象类的源代码文件并生成包含模型生成的视图的源代码文件。 有关详细信息，请参阅[Pre-Generated 映射视图](https://docs.microsoft.com/ef/ef6/fundamentals/performance/pre-generated-views)。

## <a name="related-topics"></a>相关主题

| 标题 | 描述 |
| - | - |
| [ADO.NET 实体框架](/dotnet/framework/data/adonet/ef/index) | 介绍如何使用[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)]工具，其中[!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)]提供创建应用程序。 |
| [实体数据模型](/dotnet/framework/data/adonet/entity-data-model) | 提供用于处理数据的基础上构建的应用程序使用链接和信息[!INCLUDE[adonet_ef](../data-tools/includes/adonet_ef_md.md)]。 |
| [Entity Framework (EF) 文档）](https://docs.microsoft.com/ef/ef6/get-started) | 提供的视频、 教程和高级的文档可帮助您充分利用 Entity Framework 的索引。 |
| [ASP.NET 5 应用程序指向新数据库](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html) | 介绍如何使用 Entity Framework 7 创建一个新的 ASP.NET 5 应用程序。 |

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)