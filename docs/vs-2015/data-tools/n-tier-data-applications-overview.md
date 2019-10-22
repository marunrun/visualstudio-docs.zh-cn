---
title: N 层数据应用程序概述 |Microsoft Docs
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
- presentation tier
- middle tier
- data tier
- n-tier applications, about n-tier applications
ms.assetid: 1020581d-eaaa-41a2-aca4-bf4c212895f6
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0f124e997669370e71819cf37423d0c2d6a414d7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658059"
---
# <a name="n-tier-data-applications-overview"></a>N 层数据应用程序概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

N 层 * 数据应用程序是指分为多个*层*的数据应用程序。 也称为 "分布式应用程序" 和 "多层应用程序"，n 层应用程序将处理单独处理到在客户端和服务器之间分布的离散层。 开发访问数据的应用程序时，应在构成应用程序的各个层之间明确分隔。

 典型的 n 层应用程序包括一个表示层、一个中间层和一个数据层。 分隔 n 层应用程序中各个层的最简单方法是为每个要包括在应用程序中的层创建不同的项目。 例如，表示层可能是 Windows 窗体应用程序，而数据访问逻辑可能是位于中间层的类库。 此外，表示层可以通过服务（如服务）与中间层中的数据访问逻辑通信。 将应用程序组件分离到不同的层可提高应用程序的可维护性和可伸缩性。 为实现此功能，可更轻松地采用可应用于单个层的新技术，而无需重新设计整个解决方案。 此外，n 层应用程序通常将敏感信息存储在中间层中，这会保持与表示层的隔离。

 Visual Studio 包含多项功能，可帮助开发人员创建 n 层应用程序：

- 数据集设计器提供了一个**数据集项目**属性，使您可以将数据集（数据实体层）和 `TableAdapter`s （数据访问层）分成不同的项目。

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)提供了用于将 DataContext 和数据类生成到单独命名空间中的设置。 这可以实现数据访问层和数据实体层的逻辑分离。

- [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)提供 <xref:System.Data.Linq.Table%601.Attach%2A> 方法，使你可以将应用程序中不同层的 DataContext 组合在一起。 有关详细信息，请参阅[具有 LINQ to SQL 的 N 层和远程应用程序](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)。

## <a name="presentation-tier"></a>呈现层
 *呈现层*是用户与应用程序进行交互的层。 它通常还包含其他应用程序逻辑。 典型的表示层组件包括：

- 数据绑定组件，如 <xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

- 数据的对象表示形式，例如[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)要在表示层中使用的实体类。

  呈现层通常使用服务引用访问中间层（例如，[在 Visual Studio 应用程序中 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)）。 呈现层不直接访问数据层。 呈现层通过中间层中数据访问组件的方式与数据层通信。

## <a name="middle-tier"></a>中间层
 *中间层*是表示层和数据层用来相互通信的层。 典型的中间层组件包括：

- 业务逻辑，如业务规则和数据验证。

- 数据访问组件和逻辑，如下所示：

  - [Tableadapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)和[dataadapter 和 datareader](https://msdn.microsoft.com/library/cc952ca2-ec19-46ab-9189-15174b52cb74)。

  - 数据的对象表示形式，例如[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)实体类。

  - 常见的应用程序服务，例如身份验证、授权和个性化。

  下图显示了 Visual Studio 中可用的功能和技术，以及它们可能适合于 n 层应用程序的中间层的位置。

  ![中间层组件](../data-tools/media/ntiermid.png "NtierMid")中间层

  中间层通常使用数据连接连接到数据层。 此数据连接通常存储在数据访问组件中。

## <a name="data-tier"></a>数据层
 *数据层*基本上是存储应用程序数据的服务器（例如，运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的服务器）。

 下图显示了 Visual Studio 中可用的功能和技术，以及它们可能适合 n 层应用程序的数据层的位置。

 ![数据层组件](../data-tools/media/ntierdatatier.png "ntierdatatier")数据层

 数据层无法直接从表示层中的客户端访问。 中间层中的数据访问组件用于表示层和数据层之间的通信。

## <a name="help-for-n-tier-development"></a>N 层开发帮助
 以下主题提供有关使用 n 层应用程序的信息：

 [将数据集和 TableAdapter 分离到不同的项目中](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)

 [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)

 [演练：向 N 层数据应用程序添加验证](https://msdn.microsoft.com/library/b35d072c-31f0-49ba-a225-69177592c265)

 [使用 LINQ to SQL 的 N 层和远程应用程序](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)

## <a name="see-also"></a>请参阅
 <xref:System.Data.Linq.ITable.Attach%2A> 演练：[在 Visual studio 中](../data-tools/dataset-tools-in-visual-studio.md)[创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)[分层更新](../data-tools/hierarchical-update.md)数据集工具在 visual studio 中[访问数据](../data-tools/accessing-data-in-visual-studio.md)
