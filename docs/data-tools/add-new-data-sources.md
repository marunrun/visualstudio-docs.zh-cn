---
title: 添加新数据源
ms.date: 11/21/2018
ms.topic: conceptual
f1_keywords:
- vs.datasource.datasourcefieldspicker
helpviewer_keywords:
- data [Visual Studio], data sources
- data sources
ms.assetid: ed28c625-bb89-4037-bfde-cfa435d182a2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 05a07fc3cb72f923d28ff907c9aec69620cbd40d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62824865"
---
# <a name="add-new-data-sources"></a>添加新数据源

在上下文中的.NET data tools 在 Visual Studio 中，术语*数据源*指连接到数据存储，使数据可用于.NET 应用程序的.NET 对象。 Visual Studio 设计器可以使用数据源以生成将数据绑定到窗体上，拖动并放置中的数据库对象时的样板代码的输出**数据源**窗口。 此类数据源可以是：

- 与某种类型的数据库相关联的实体框架模型中的类。

- 一个与某种类型的数据库相关联的数据集。

- 一个表示 Windows Communication Foundation (WCF) 数据服务或 REST 服务之类的网络服务的类。

- 一个表示 SharePoint 服务的类。

- 类或你的解决方案中的集合。

> [!NOTE]
> 如果您不使用数据绑定功能，则不适用的数据集、 实体框架中，LINQ to SQL，WCF 或 SharePoint，"数据源"的概念。 只需通过直接连接到该数据库使用 SQLCommand 对象并直接与数据库通信。

创建和编辑数据源使用**数据源配置向导**Windows 窗体或 Windows Presentation Foundation 应用程序中。 有关实体框架中，首先创建实体类，并选择，然后启动向导**项目** > **添加新数据源**（本文后面的更多详细信息中所述）。

![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)

## <a name="data-sources-window"></a>“数据源”窗口

创建数据源后，它将出现在**数据源**工具窗口。

> [!TIP]
> 若要打开**数据源**窗口中，请确保你的项目处于打开状态，，然后按**Shift**+**Alt**+**D**或选择**视图** > **其他 Windows** > **数据源**。

可以将从数据源**数据源**窗口拖到窗体设计图面或控件。 这将导致样板文件代码以生成，显示从数据存储的数据。

下图显示了已删除 Windows 窗体上的数据集。 如果选择**F5**应用程序，从基础数据库的数据显示在窗体的控件。

![数据源拖放操作](../data-tools/media/raddata-data-source-drag-operation.png)

## <a name="data-source-for-a-database-or-a-database-file"></a>为数据库或数据库文件的数据源

可以创建数据集或实体框架模型作为数据源使用的数据库或数据库文件。

### <a name="dataset"></a>数据集

若要创建一个数据集作为数据源，运行**数据源配置向导**通过选择**项目** > **添加新数据源**。 选择**数据库**数据源类型，并按照提示来指定新的或现有的数据库连接或数据库文件。

### <a name="entity-classes"></a>实体类

若要创建的实体框架模型作为数据源：

1. 运行**实体数据模型向导**创建实体类。 选择**项目** > **添加新项** > **ADO.NET 实体数据模型**。

   ![新的实体框架模型项目项](../data-tools/media/raddata-new-entity-framework-model-project-item.png)

1. 选择你想要生成的模型的方法。

   ![实体数据模型向导](../data-tools/media/raddata-entity-data-model-wizard.png)

1. 将模型添加为数据源。 生成的类显示在**数据源配置向导**选择时**对象**类别。

   ![与实体类的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-entity-classes.png)

## <a name="data-source-for-a-service"></a>一种服务的数据源

若要从服务中创建数据源，运行**数据源配置向导**，然后选择**服务**数据源类型。 这是快捷方式**添加服务引用**对话框中，还可以通过右键单击该项目中的访问**解决方案资源管理器**，然后选择**添加服务引用**.

在从服务创建数据源，Visual Studio 将添加到你的项目的服务引用。 Visual Studio 还会创建对应于该服务返回的对象的代理对象。 例如，返回的数据集的服务都在你的项目作为为数据集返回作为类型在项目中表示特定类型返回服务。

可以从以下类型的服务创建数据源：

- [WCF Data Services](/dotnet/framework/data/wcf/wcf-data-services-overview)

- [WCF 服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

- Web 服务

    > [!NOTE]
    > 在显示的项**数据源**窗口都依赖于该服务返回的数据。 某些服务可能没有为“数据源配置”向导创建可绑定的对象提供足够的信息。 例如，如果该服务返回的非类型化数据集，显示任何项中**数据源**窗口时完成该向导。 这是因为非类型化数据集不提供架构，因此该向导没有足够的信息来创建数据源。

## <a name="data-source-for-an-object"></a>一个对象的数据源

可以从任何通过运行公开一个或多个公共属性的对象创建数据源**数据源配置向导**，然后选择**对象**数据源类型。 一个对象的所有公共属性显示在**数据源**窗口。 如果在使用实体框架，并且已生成一个模型，这是在哪里找到你的应用程序的数据源的实体类。

上**选择数据对象**页上，展开树视图，找到你想要将绑定到的对象中的节点。 在树视图包含节点为你的项目和程序集和由项目引用其他项目。

如果你想要将绑定到程序集或项目未显示在树视图中的对象，请单击**添加引用**并用**添加引用对话框**以添加对程序集或项目的引用。 添加引用后，程序集或项目添加到树视图。

> [!NOTE]
> 您可能需要生成项目之前在树视图中显示这些对象包含您的对象。

> [!NOTE]
> 若要支持拖放数据绑定对象实现<xref:System.ComponentModel.ITypedList>或<xref:System.ComponentModel.IListSource>接口必须具有默认构造函数。 否则为 Visual Studio 无法实例化的数据源对象，并将项拖至设计图面上时显示错误。

## <a name="data-source-for-a-sharepoint-list"></a>SharePoint 列表数据源

可以从 SharePoint 列表创建数据源，通过运行**数据源配置向导**，然后选择**SharePoint**数据源类型。 SharePoint 通过 WCF Data Services 将数据公开，因此创建 SharePoint 数据源是从服务中创建数据源相同。 选择**SharePoint**中的项**数据源配置向导**打开**添加服务引用**对话框中，连接到 SharePoint 数据服务的位置通过指向 SharePoint 服务器。 这要求 SharePoint SDK。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)