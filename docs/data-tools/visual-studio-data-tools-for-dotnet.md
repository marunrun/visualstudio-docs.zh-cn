---
title: 适用于.NET 的数据工具
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
- dotnet
ms.openlocfilehash: a4a62f629244d44680b3d5ac3233bd45b975302e
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66745310"
---
# <a name="visual-studio-data-tools-for-net"></a>适用于 NET 的 Visual Studio Data Tools

Visual Studio 和.NET 一起提供广泛的 API 和工具连接到数据库、 在内存中，数据建模和用户界面中显示数据的支持。 提供数据访问功能的.NET 类名为[ADO.NET](/dotnet/framework/data/adonet/index)。 ADO.NET 中的，以及数据工具在 Visual Studio 中，主要设计用于支持关系数据库和 XML。 如今，许多 NoSQL 数据库供应商或第三方提供 ADO.NET 提供程序。

[.NET core](/dotnet/core/)支持 ADO.NET，数据集和其相关的类型除外。 如果要面向.NET Core，并且需要一个对象关系映射 (ORM) 层，使用[Entity Framework Core](/ef/core/)。

下图显示了基本的体系结构的简化的视图：

![ADO.NET 体系结构](../data-tools/media/raddata-ado-net-architecture-diagram.png)

## <a name="typical-workflow"></a>典型的工作流

这是典型的工作流：

1. 在本地计算机上安装开发或测试数据库。 请参阅[安装数据库系统、 工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)。 如果使用 Azure 数据服务，此步骤不是必需的。

2. 在 Visual Studio 中测试与数据库 （或服务或本地文件） 的连接。 请参阅[添加新连接](../data-tools/add-new-connections.md)。

3. （可选）使用工具来生成和配置新的模型。 基于实体框架的模型是新的应用程序的默认建议。 模型中，使用，无论哪一个是应用程序与之进行交互的数据源。 该模型在逻辑上位于数据库或服务与应用程序之间。 请参阅[添加新数据源](../data-tools/add-new-data-sources.md)。

4. 从数据源拖动**数据源**窗口拖到 Windows 窗体、 ASP.NET 或 Windows Presentation Foundation 设计图面上以生成将在你指定的方式向用户显示的数据的数据绑定代码。 请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

5. 添加自定义代码的内容，如业务规则、 搜索和数据验证，或若要充分利用基础数据库公开的自定义功能。

可以跳过步骤 3 和.NET 应用程序发出命令直接向数据库中，而不是使用模型进行编程。 在这种情况下，您将找到相关文档：[ADO.NET](/dotnet/framework/data/adonet/index)。 请注意，仍可以使用**数据源配置向导**和设计器来填充您自己的内存，然后将 UI 控件数据绑定到这些对象中的对象时生成数据绑定代码。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)