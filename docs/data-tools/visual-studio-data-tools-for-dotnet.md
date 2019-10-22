---
title: 适用于 .NET 的数据工具
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
- dotnet
ms.openlocfilehash: 224fef3a02a2441553728a9a75fc5f9c456081a1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648092"
---
# <a name="visual-studio-data-tools-for-net"></a>适用于 NET 的 Visual Studio Data Tools

Visual Studio 和 .NET 共同提供了广泛的 API 和工具支持，用于连接到数据库、对内存中的数据进行建模，以及在用户界面中显示数据。 提供数据访问功能的 .NET 类称为[ADO.NET](/dotnet/framework/data/adonet/index)。 ADO.NET 与 Visual Studio 中的数据工具一起设计，主要用于支持关系数据库和 XML。 如今，许多 NoSQL 数据库供应商或第三方提供 ADO.NET 提供商。

除数据集及其相关类型之外， [.Net Core](/dotnet/core/)还支持 ADO.NET。 如果面向的是 .NET Core 并且需要对象关系映射（ORM）层，请使用[Entity Framework Core](/ef/core/)。

下图显示了基本体系结构的简化视图：

![ADO.NET 体系结构](../data-tools/media/raddata-ado-net-architecture-diagram.png)

## <a name="typical-workflow"></a>典型工作流

典型的工作流如下所示：

1. 在本地计算机上安装开发或测试数据库。 请参阅[安装数据库系统、工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)。 如果你使用的是 Azure 数据服务，则不需要执行此步骤。

2. 在 Visual Studio 中测试与数据库（或服务或本地文件）的连接。 请参阅[添加新连接](../data-tools/add-new-connections.md)。

3. 可有可无使用工具生成和配置新的模型。 基于实体框架的模型是新应用程序的默认建议。 使用的模型是应用程序与之交互的数据源。 模型在逻辑上位于数据库或服务与应用程序之间。 请参阅[添加新数据源](../data-tools/add-new-data-sources.md)。

4. 将数据源从 "**数据源**" 窗口拖动到 Windows 窗体、ASP.NET 或 Windows Presentation Foundation 设计图面上，以生成将按你指定的方式向用户显示数据的数据绑定代码。 请参阅[在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

5. 为业务规则、搜索和数据验证等项目添加自定义代码，或利用基础数据库公开的自定义功能。

您可以跳过步骤3，并对 .NET 应用程序进行编程以直接向数据库发出命令，而不使用模型。 在这种情况下，您将找到相关文档：[ADO.NET](/dotnet/framework/data/adonet/index)。 请注意，在内存中填充自己的对象，然后将数据绑定 UI 控件数据绑定到这些对象时，仍可以使用 "**数据源配置向导**" 和 "设计器" 生成数据绑定代码。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)