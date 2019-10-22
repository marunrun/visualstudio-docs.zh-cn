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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 99e9d9d466ae32d86b64b17738c96c245bda8f96
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648888"
---
# <a name="add-new-data-sources"></a>添加新数据源

在 Visual Studio 中的 .NET data tools 的上下文中，术语 "*数据源*" 是指连接到数据存储的 .net 对象，并使数据可用于 .net 应用程序。 当您在 "**数据源**" 窗口中拖放数据库对象时，Visual Studio 设计器可以使用数据源的输出生成将数据绑定到窗体的样板代码。 这种类型的数据源可以是：

- 与某种数据库相关联的实体框架模型中的类。

- 与某种数据库相关联的数据集。

- 表示网络服务（例如 Windows Communication Foundation （WCF）数据服务或 REST 服务）的类。

- 表示 SharePoint 服务的类。

- 解决方案中的类或集合。

> [!NOTE]
> 如果未使用数据绑定功能、数据集、实体框架、LINQ to SQL、WCF 或 SharePoint，则 "数据源" 的概念不适用。 只需使用 SQLCommand 对象直接连接到数据库，并直接与数据库进行通信。

您可以使用 Windows 窗体或 Windows Presentation Foundation 应用程序中的 "**数据源配置向导**" 来创建和编辑数据源。 对于实体框架，请先创建实体类，然后通过选择 "**项目**"  >  "**添加新数据源**" （本文稍后将详细介绍）来启动向导。

![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)

## <a name="data-sources-window"></a>“数据源”窗口

创建数据源后，它将显示在 "**数据源**" 工具窗口中。

> [!TIP]
> 若要打开 "**数据源**" 窗口，请确保您的项目已打开，然后按**Shift** +**Alt** +**D**或选择 "**查看** > **其他 Windows**  > **数据源**"。

您可以将数据源从 "**数据源**" 窗口拖到窗体设计图面或控件上。 这将导致生成用于显示来自数据存储的数据的样板代码。

下图显示了已拖放到 Windows 窗体上的数据集。 如果在应用程序上选择 " **F5** "，则基础数据库中的数据将显示在窗体的控件中。

![数据源拖动操作](../data-tools/media/raddata-data-source-drag-operation.png)

## <a name="data-source-for-a-database-or-a-database-file"></a>数据库或数据库文件的数据源

您可以创建数据集或实体框架模型，用作数据库或数据库文件的数据源。

### <a name="dataset"></a>数据集

若要创建数据集作为数据源，请通过选择 "**项目**"  >  "**添加新数据源**"，运行 "**数据源配置向导**"。 选择**数据库**数据源类型，然后按照提示指定新的或现有的数据库连接或数据库文件。

### <a name="entity-classes"></a>实体类

若要创建实体框架模型作为数据源：

1. 运行**实体数据模型向导**创建实体类。 选择**项目** >  "**添加新项**"  > **ADO.NET 实体数据模型**"。

   ![新建实体框架模型项目项](../data-tools/media/raddata-new-entity-framework-model-project-item.png)

1. 选择要用来生成模型的方法。

   ![实体数据模型向导](../data-tools/media/raddata-entity-data-model-wizard.png)

1. 添加模型作为数据源。 当您选择 "**对象**" 类别时，生成的类将出现在 "**数据源配置向导**" 中。

   ![具有实体类的数据源配置向导](../data-tools/media/raddata-data-source-configuration-wizard-with-entity-classes.png)

## <a name="data-source-for-a-service"></a>服务的数据源

若要从服务创建数据源，请运行 "**数据源配置向导**" 并选择 "**服务**数据源类型"。 这只是**添加服务引用**对话框的快捷方式，您还可以通过右键单击**解决方案资源管理器**中的项目并选择 "**添加服务引用**" 来访问该对话框。

当您从服务创建数据源时，Visual Studio 会向您的项目中添加一个服务引用。 Visual Studio 还会创建与服务返回的对象相对应的代理对象。 例如，返回数据集的服务在项目中表示为数据集;返回特定类型的服务在项目中表示为返回的类型。

可以从以下类型的服务创建数据源：

- [WCF Data Services](/dotnet/framework/data/wcf/wcf-data-services-overview)

- [WCF 服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

- Web 服务

    > [!NOTE]
    > "**数据源**" 窗口中显示的项取决于服务返回的数据。 某些服务可能没有为“数据源配置”向导创建可绑定的对象提供足够的信息。 例如，如果服务返回非类型化数据集，则在完成该向导时，"**数据源**" 窗口中将不会显示任何项。 这是因为非类型化数据集不提供架构，因此该向导没有足够的信息来创建数据源。

## <a name="data-source-for-an-object"></a>对象的数据源

您可以通过运行 "**数据源配置向导**"，然后选择**对象**数据源类型，从公开一个或多个公共属性的任何对象创建数据源。 对象的所有公共属性都显示在 "**数据源**" 窗口中。 如果使用实体框架并且生成了模型，则可以在此查找作为应用程序的数据源的实体类。

在 "**选择数据对象**" 页上，展开树视图中的节点以查找要绑定到的对象。 树视图包含您的项目的节点以及您的项目所引用的程序集和其他项目。

如果要绑定到树视图中未显示的程序集或项目中的对象，请单击 "**添加引用**"，并使用 "**添加引用" 对话框**添加对程序集或项目的引用。 添加引用后，程序集或项目将添加到树视图中。

> [!NOTE]
> 在树视图中显示对象之前，你可能需要生成包含对象的项目。

> [!NOTE]
> 若要支持拖放数据绑定，实现 <xref:System.ComponentModel.ITypedList> 或 <xref:System.ComponentModel.IListSource> 接口的对象必须具有默认构造函数。 否则，Visual Studio 无法实例化数据源对象，并在将项拖动到设计图面时显示错误。

## <a name="data-source-for-a-sharepoint-list"></a>SharePoint 列表的数据源

通过运行 "**数据源配置向导**" 并选择 " **sharepoint**数据源类型"，可以从 SharePoint 列表创建数据源。 SharePoint 通过 WCF 数据服务公开数据，因此创建 SharePoint 数据源与从服务创建数据源相同。 在 "**数据源配置向导**" 中选择**SharePoint**项将打开 "**添加服务引用**" 对话框，在该对话框中，您可以通过指向 sharepoint 服务器来连接到 sharepoint 数据服务。 这需要 SharePoint SDK。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)