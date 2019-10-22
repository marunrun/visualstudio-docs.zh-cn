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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d663b86603145f8a665f189e5abfbfa2b0b360ae
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672384"
---
# <a name="entity-data-model-tools-in-visual-studio"></a>Visual Studio 中的实体数据模型工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

实体框架是一种对象关系映射技术，它使 .NET 开发人员能够使用特定于域的对象处理关系数据。 它不要求提供开发人员通常需要编写的大部分数据访问代码。 对于新的 .NET 应用程序，实体框架是建议的对象关系映射（ORM）建模技术。

 从2016年3月起，最新发布的版本为[实体框架 6](https://msdn.microsoft.com/data/ef) 。 [实体框架 7](https://docs.efproject.net/en/latest/)处于预发行版本中。

 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] 工具旨在帮助您构建 [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] 应用程序。 @No__t_0 工具的完整文档位于此处：[实体框架](https://msdn.microsoft.com/data/jj590134)。

 使用 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] 工具，可以从现有数据库创建*概念模型*，然后以图形方式直观显示和编辑概念模型。 或者，您可以首先以图形方式创建概念模型，然后生成支持模型的数据库。 无论哪种情况，你都可以在基础数据库更改时自动更新模型，并为应用程序生成对象层代码。 数据库生成和对象层代码生成是可自定义的。

 这些是在 Visual Studio 2015 中构成实体数据模型工具的特定工具：

- 您可以使用 [!INCLUDE[vstecado](../includes/vstecado-md.md)] **[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] 设计器**（**Entity Designer**）直观地创建和修改实体、关联、映射以及继承关系。 **Entity Designer**还会生成 [!INCLUDE[TLA#tla_cshrp](../includes/tlasharptla-cshrp-md.md)] 或 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 的对象层代码。

- 您可以使用 **[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] 向导**通过现有数据库生成概念模型，并将数据库连接信息添加到您的应用程序。

- 您可以使用 "**创建数据库向导**" 先创建概念模型，然后创建支持该模型的数据库。

- 在对基础数据库进行更改后，可以使用**模型更新向导**来更新概念模型、存储模型和映射。

  > [!NOTE]
  > 从 Visual Studio 2010 开始，[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] 工具不支持 [!INCLUDE[ss2k](../includes/ss2k-md.md)]。

  这些工具可生成或修改 .edmx 文件。 此文件包含描述概念模型、存储模型和这些模型之间的映射的信息。 有关详细信息，请参阅[EDMX](https://msdn.microsoft.com/data/jj650889.aspx)。

  实体框架 Power Tools 可帮助生成使用实体数据模型的应用程序。 这些工具可生成概念模型、验证现有模型、生成包含基于概念模型的对象类的源代码文件，并生成包含模型生成的视图的源代码文件。 有关详细信息，请参阅[预生成的映射视图](https://msdn.microsoft.com/data/dn469601.aspx)。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[ADO.NET 实体框架](https://msdn.microsoft.com/library/a437041f-6899-4ae7-96ce-aabf528d7205)|描述如何使用 [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] 提供的 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] 工具来创建应用程序。|
|[实体数据模型](https://msdn.microsoft.com/library/2dda3d5b-4582-4ba0-a91d-fcd7a1498137)|提供有关使用 [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] 上构建的应用程序所使用的数据的链接和信息。|
|[完整 .NET 上的入门（控制台、WinForms、WPF 等）](/ef/ef6/get-started)|提供有关如何创建使用实体框架7的 .NET 桌面应用程序的教程。|
|[ASP.NET 5 应用程序到新数据库](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html)|介绍如何使用实体框架7创建新的 ASP.NET 5 应用程序。|

## <a name="see-also"></a>请参阅
 [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
