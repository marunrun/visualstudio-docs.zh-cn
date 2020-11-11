---
title: N 层数据应用程序概述
description: 阅读 N 层数据应用程序概述。 也称为分布式应用程序或多层应用程序，它们是分为多个层的数据应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- presentation tier
- middle tier
- data tier
- n-tier applications, about n-tier applications
ms.assetid: 1020581d-eaaa-41a2-aca4-bf4c212895f6
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ea1ab222868df6ff1b22eee7827e1edd3978a88e
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436206"
---
# <a name="n-tier-data-applications-overview"></a>N 层数据应用程序概述
N 层数据应用程序是分为多个层的数据应用程序 。 n 层应用程序亦称为“分散式应用程序”和“多层应用程序”，可以将处理操作分离到独立的层中，这些层分散在客户端和服务器之间。 开发访问数据的应用程序时，应在构成应用程序的各个层之间进行明确的分离。

典型的 n 层应用程序包括一个表示层、一个中间层和一个数据层。 在 n 层应用程序中，分离各层的最简单的方法是为要包括在应用程序中的每一层创建相互独立的项目。 例如，表示层可能是 Windows 窗体应用程序，而数据访问逻辑可能是位于中间层的类库。 此外，表示层可通过 Web 服务等服务与中间层中的数据访问逻辑进行通信。 将应用程序组件分离到不同的层可提高应用程序的可维护性和可伸缩性。 该结构之所以具有这种优点，是因为它能轻松采用可应用于单个层而无需重新设计整个解决方案的新技术。 此外，n 层应用程序通常将敏感信息存储在中间层中，从而与表示层保持隔离。

Visual Studio 包含多个功能，可帮助开发人员创建 n 层应用程序：

- 数据集提供“数据集项目”属性，支持将数据集（数据实体层）和 TableAdapters（数据访问层）分离到独立的项目中。

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)提供用于在单独的命名空间中生成 DataContext 和数据类的设置。 这可实现数据访问层和数据实体层的逻辑分离。

- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) 提供 <xref:System.Data.Linq.Table%601.Attach%2A> 方法，可用于将应用程序中不同层的 DataContext 组合在一起。 有关详细信息，请参阅[使用 LINQ to SQL 的 N 层和远程应用程序](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)。

## <a name="presentation-tier"></a>呈现层
表示层是用户与应用程序进行交互的层。 它通常也包含其他应用程序逻辑。 典型的表示层组件包括以下内容：

- 数据绑定组件，如 <xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

- 数据的对象表示形式，如用于表示层的 [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) 实体类。

表示层通常通过使用服务引用（例如 [Visual Studio 应用程序中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)）来访问中间层。 表示层无法直接访问数据层。 表示层通过中间层中的数据访问组件与数据层进行通信。

## <a name="middle-tier"></a>中间层
中间层是表示层和数据层用来相互通信的层级。 典型的中间层组件包括以下内容：

- 业务逻辑，例如业务规则和数据验证。

- 数据访问组件和逻辑，例如：

  - [TableAdapters](create-and-configure-tableadapters.md) 及 [DataAdapters 和 DataReaders](/dotnet/framework/data/adonet/dataadapters-and-datareaders)。

  - 数据的对象表示形式，如 [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) 实体类。

  - 常用应用程序服务，如身份验证、授权和个性化。

下图显示 Visual Studio 中可用的功能和技术，以及它们在哪些场景下可能适用于 n 层应用程序的中间层。

![中间层组件](../data-tools/media/ntiermid.png) 中间层

中间层通常通过使用数据连接来连接到数据层。 此数据连接通常存储在数据访问组件中。

## <a name="data-tier"></a>数据层
数据层是存储应用程序数据的服务器（例如运行 SQL Server 的服务器）。

下图显示 Visual Studio 中可用的功能和技术，以及它们在哪些场景下可能适用于 n 层应用程序的数据层。

![数据层组件](../data-tools/media/ntierdatatier.png) 数据层

无法直接从表示层中的客户端访问数据层。 取而代之的是，中间层的数据访问组件用于表示层和数据层之间的通信。

## <a name="help-for-n-tier-development"></a>帮助进行 n 层开发
以下主题提供有关开发 n 层应用程序的信息：

[将数据集和 TableAdapter 分离到不同的项目中](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)

[演练：创建 n 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)

[使用 LINQ to SQL 的 n 层和远程应用程序](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)

## <a name="see-also"></a>另请参阅

- [演练：创建 n 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
