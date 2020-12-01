---
title: 将业务数据集成到 SharePoint 中 | Microsoft Docs
description: 阅读有关如何通过为Business Data Connectivity (BDC) Service 创建模型来将业务数据集成到 SharePoint 中的简要摘要。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], business data
- BDC [SharePoint development in Visual Studio], aggregating data
- BDC [SharePoint development in Visual Studio], business data
- Business Data Connectivity service [SharePoint development in Visual Studio], aggregating data
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], data
- BDC [SharePoint development in Visual Studio], data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f3156adc286222282ae63f70f70838bc6b7155a8
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304347"
---
# <a name="integrate-business-data-into-sharepoint"></a>将业务数据集成到 SharePoint 中
  你可以将业务数据集成到 SharePoint 中。 业务数据可以来自后端服务器应用程序，如 [!INCLUDE[TLA#tla_sqlsvr](../sharepoint/includes/tlasharptla-sqlsvr-md.md)]、Siebel、SAP 或 Web 服务。 用户可以通过在 SharePoint 中使用外部列表或业务数据 Web 部件来查看、添加、更新或删除业务数据。  用户还可以在 Microsoft Office 应用程序（如 Microsoft Outlook）中离线访问此数据。 有关详细信息，请参阅[可显示外部数据的位置](/previous-versions/office/developer/sharepoint-2010/ee558737(v=office.14))。

 若要将数据集成到 SharePoint 中，请为业务数据连接 (BDC) 服务创建模型。 BDC 服务是 SharePoint 中的一个应用程序，用于存储有关业务应用程序中数据的信息。 有关详细信息，请参阅[业务数据连接 (BDC) 服务](/previous-versions/office/developer/sharepoint-2010/ee556407(v=office.14))。

## <a name="models-in-visual-studio"></a>Visual Studio 中的模型
 使用 Visual Studio 中的模型，可以编写自定义代码，以便从后端数据源检索和更新数据。 还可以聚合来自多个数据源的数据。 例如，可以显示客户列表，该列表包含来自 [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)] 数据库和 Web 服务的数据。

 还可以导入已部署到 SharePoint 中的模型。 导入模型后，可以添加自定义代码，也可以仅使用 Visual Studio 将模型打包并部署到多个 SharePoint 服务器场。 有关详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

## <a name="design-a-model-in-visual-studio"></a>在 Visual Studio 中设计模型
 可以使用设计器和多个工具窗口来设计模型。 设计模型时，Visual Studio 将生成模型 XML。 有关详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

 模型包含实体和方法。

### <a name="entities"></a>实体
 实体描述字段的集合。 例如，实体可以表示数据库中的表。 实体在 SharePoint 中显示为外部内容类型。 有关外部内容类型的详细信息，请参阅[什么是外部内容类型？](/previous-versions/office/developer/sharepoint-2010/ee556391(v=office.14))

### <a name="methods"></a>方法
 通过使用方法，外部内容类型的使用者可以对实体的字段执行操作。 例如，Updater 方法使用户能够更改客户的地址和出生日期，其中 `Address` 和 `BirthDate` 是 `Customer` 实体的字段。

 Visual Studio 将为模型中的每个实体生成一个服务代码文件。 向模型添加方法时，Visual Studio 会在服务代码文件中生成相应的方法。 向每个方法添加代码以执行相应的任务。 例如，如果将 Creator 方法添加到模型，则 Visual Studio 将在你的服务代码文件中生成一个 Creator 方法。 当用户在基于模型的列表中单击“新建项”按钮时，BDC 服务将调用此方法。 因此，向 Creator 方法添加代码，该方法可向数据源添加新数据。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)|说明如何创建新模型或导入从 SharePoint 导出的模型。|
|[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)|介绍如何使用 Visual Studio 设计工具设计模型的元素。|
|[使用 BCS 构建解决方案时，何时使用 SharePoint Designer 和 Visual Studio](/previous-versions/office/developer/sharepoint-2010/ee558875(v=office.14))|帮助你决定是使用 Visual Studio 还是使用 SharePoint Designer 来为 BDC 创建模型。|
