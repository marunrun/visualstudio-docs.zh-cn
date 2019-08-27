---
title: 实体数据模型工具
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: da608c7f937a09d56b25b87625580e5047d560cc
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705044"
---
# <a name="entity-data-model-tools-in-visual-studio"></a>在 Visual Studio 中的实体数据模型工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Entity Framework 是一种对象关系映射技术，使.NET 开发人员能够通过使用特定于域的对象处理关系数据。 它不要求提供开发人员通常需要编写的大部分数据访问代码。 实体框架是建模技术，用于新的.NET 应用程序的建议的对象关系映射 (ORM)。

 截至 2016 年 3 月发布的最新版本是[Entity Framework 6](https://msdn.microsoft.com/data/ef) 。 [Entity Framework 7](https://docs.efproject.net/en/latest/)处于预发布阶段。

 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] 工具旨在帮助您构建[!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)]应用程序。 有关完整文档[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]工具是此处：[实体框架](https://msdn.microsoft.com/data/jj590134)。

 与[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]工具，可以创建*概念模型*从现有数据库，然后以图形方式直观显示和编辑概念模型。 或者，您可以首先以图形方式创建概念模型，然后生成支持模型的数据库。 无论哪种情况，你都可以在基础数据库更改时自动更新模型，并为应用程序生成对象层代码。 数据库生成和对象层代码生成是可自定义的。

 这些是组成 Visual Studio 2015 中的实体数据模型工具的特定工具：

- 可以使用[!INCLUDE[vstecado](../includes/vstecado-md.md)]  **[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]设计器**(**实体设计器**) 直观地创建和修改实体、 关联、 映射和继承关系。 **实体设计器**还会生成[!INCLUDE[TLA#tla_cshrp](../includes/tlasharptla-cshrp-md.md)]或[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]对象层代码。

- 可以使用 **[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]向导**从现有数据库生成概念模型并将数据库连接信息添加到你的应用程序。

- 可以使用**创建数据库向导**首先创建概念模型，然后创建支持该模型的数据库。

- 可以使用**模型更新向导**基础数据库发生更改时，更新概念模型、 存储模型和映射。

  > [!NOTE]
  > 从 Visual Studio 2010，开始[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]工具不支持[!INCLUDE[ss2k](../includes/ss2k-md.md)]。

  这些工具生成或修改.edmx 文件。 此文件包含描述概念模型、 存储模型中，以及它们之间的映射的信息。 有关详细信息，请参阅[EDMX](https://msdn.microsoft.com/data/jj650889.aspx)。

  Entity Framework Power Tools 帮助您生成使用实体数据模型的应用程序。 这些工具可以生成概念模型、 验证现有模型、 生成包含基于概念模型中，对象类的源代码文件并生成包含模型生成的视图的源代码文件。 有关详细信息，请参阅[Pre-Generated 映射视图](https://msdn.microsoft.com/data/dn469601.aspx)。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[ADO.NET 实体框架](https://msdn.microsoft.com/library/a437041f-6899-4ae7-96ce-aabf528d7205)|介绍如何使用[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]工具，其中[!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)]提供创建应用程序。|
|[实体数据模型](https://msdn.microsoft.com/library/2dda3d5b-4582-4ba0-a91d-fcd7a1498137)|提供用于处理数据的基础上构建的应用程序使用链接和信息[!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)]。|
|[完整的.NET （控制台、 WinForms、 WPF 等） 上开始使用](/ef/ef6/get-started)|有关如何创建使用 Entity Framework 7 的.NET 桌面应用程序提供的教程。|
|[ASP.NET 5 应用程序指向新数据库](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html)|介绍如何使用 Entity Framework 7 创建一个新的 ASP.NET 5 应用程序。|

## <a name="see-also"></a>请参阅
 [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
