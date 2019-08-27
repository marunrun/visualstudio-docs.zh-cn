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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d54d69a9aeda76c79208c2685efde94eaaab1017
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65693775"
---
# <a name="n-tier-data-applications-overview"></a>N 层数据应用程序概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

N-层 * 数据应用程序是数据应用程序，分为多个*层*。 也称为"分布式应用程序"和"多层应用程序"，n 层应用程序分离到相互独立的层的客户端和服务器之间分布处理。 当开发访问数据的应用程序时，应清楚地区分组成应用程序的各个层。  
  
 典型的 n 层应用程序包括一个表示层、一个中间层和一个数据层。 单独的 n 层应用程序中的各个层的最简单方法是创建每个层都想要包括在应用程序中的离散项目。 例如，表示层可能是 Windows 窗体应用程序，而数据访问逻辑可以是位于中间层中的类库。 此外，表示层可能与数据访问逻辑在中间层通过服务之类的服务通信。 将应用程序组件分离到不同的层可提高应用程序的可维护性和可伸缩性。 有利于采用新技术，可应用于单个层而无需重新设计整个解决方案执行此操作。 此外，n 层应用程序通常将敏感信息存储在中间层中，以便与表示层隔离。  
  
 Visual Studio 包含多种功能，可帮助开发人员创建 n 层应用程序：  
  
- 数据集设计器提供了**数据集项目**属性，可用于单独的数据集 （数据实体层） 和`TableAdapter`s （数据访问层） 相互独立的项目。  
  
- [LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)提供了单独的命名空间中生成的 DataContext 和数据类的设置。 这样，数据访问和数据实体层的逻辑分隔。  
  
- [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)提供了<xref:System.Data.Linq.Table%601.Attach%2A>方法，可用于从应用程序中的不同层将组合在一起的 DataContext。 有关详细信息，请参阅[N 层和远程应用程序使用 LINQ 到 SQL](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)。  
  
## <a name="presentation-tier"></a>表示层  
 *表示层*是用户与应用程序交互的层。 它通常还包含其他应用程序逻辑。 典型的表示层组件包括：  
  
- 数据绑定组件，如<xref:System.Windows.Forms.BindingSource>和<xref:System.Windows.Forms.BindingNavigator>。  
  
- 对象表示的数据，例如[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)表示层中使用的实体类。  
  
  表示层通常通过使用服务引用来访问中间层 (例如， [Windows Communication Foundation 服务和 Visual Studio 中的 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)应用程序)。 表示层不直接访问数据层。 表示层与数据层通过中间层中的数据访问组件进行通信。  
  
## <a name="middle-tier"></a>中间层  
 *中间层*表示层与数据层的层用于相互通信。 典型的中间层组件包括：  
  
- 业务逻辑，例如业务规则和数据验证。  
  
- 数据访问组件和逻辑，如下所示：  
  
  - [Tableadapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)并[Dataadapter 和 Datareader](https://msdn.microsoft.com/library/cc952ca2-ec19-46ab-9189-15174b52cb74)。  
  
  - 对象表示的数据，例如[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)实体类。  
  
  - 常见的应用程序服务，例如身份验证、 授权和个性化设置。  
  
  下图显示了功能和技术，可在 Visual Studio 中以及其中它们可能适合为 n 层应用程序的中间层。  
  
  ![中间层组件](../data-tools/media/ntiermid.png "NtierMid")  
  中间层  
  
  中间层通常可以通过使用数据连接连接到数据层。 此数据连接通常存储在数据访问组件。  
  
## <a name="data-tier"></a>数据层  
 *数据层*基本上是将应用程序的数据存储在服务器 (例如，运行的服务器[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])。  
  
 下图显示了功能和技术，可在 Visual Studio 中以及其中它们可能适合为 n 层应用程序的数据层。  
  
 ![数据层组件](../data-tools/media/ntierdatatier.png "ntierdatatier")  
数据层  
  
 不能直接从表示层中的客户端访问的数据层。 相反，中间层中的数据访问组件用于演示文稿和数据层之间的通信。  
  
## <a name="help-for-n-tier-development"></a>关于 N 层开发的帮助  
 以下主题提供有关使用 n 层应用程序的信息：  
  
 [将数据集和 TableAdapter 分离到不同的项目中](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)  
  
 [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)  
  
 [演练：向 N 层数据应用程序中添加验证](https://msdn.microsoft.com/library/b35d072c-31f0-49ba-a225-69177592c265)  
  
 [使用 LINQ to SQL 的 N 层和远程应用程序](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Data.Linq.ITable.Attach%2A>   
 [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)   
 [分层更新](../data-tools/hierarchical-update.md)   
 [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)   
 [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
