---
title: 将业务数据集成到 SharePoint |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: fbbdba27b5ccc52e64575aad018af4ca20cf2e14
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008764"
---
# <a name="integrate-business-data-into-sharepoint"></a>将业务数据集成到 SharePoint
  可以将业务数据集成到 SharePoint。 业务数据可以来源于后端服务器应用程序，如[!INCLUDE[TLA#tla_sqlsvr](../sharepoint/includes/tlasharptla-sqlsvr-md.md)]，Siebel，SAP，或 Web 服务。 用户可以查看、 添加、 更新或通过使用外部列表或业务数据 Web 部件在 SharePoint 中删除的业务数据。  用户也可以访问此数据的 Microsoft Office 应用程序，例如 Microsoft Outlook 中脱机。 有关详细信息，请参阅[其中可以显示外部数据的](http://go.microsoft.com/fwlink/?LinkId=169295)。

 若要将数据集成到 SharePoint，创建业务数据连接 (BDC) 服务的模型。 BDC 服务是 SharePoint 中的业务应用程序中存储数据的信息的应用程序。 有关详细信息，请参阅[业务数据连接 (BDC) 服务](http://go.microsoft.com/fwlink/?LinkID=169276)。

## <a name="models-in-visual-studio"></a>在 Visual Studio 中的模型
 在 Visual Studio 中的模型，您可以编写自定义代码来检索和更新来自后端数据源的数据。 您还可以从多个数据源的聚合数据。 例如，可以显示一个包含中的数据的客户列表[!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]数据库和 Web 服务。

 此外可以导入已部署到 SharePoint 的模型。 导入模型之后，可以添加自定义代码或只需使用 Visual Studio 打包和将模型部署到多个 SharePoint 服务器场。 有关详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

## <a name="design-a-model-in-visual-studio"></a>设计 Visual Studio 中的模型
 可以通过使用设计器和多个工具窗口设计模型。 在设计模型时，Visual Studio 将生成 XML 的模型。 有关详细信息，请参阅[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

 模型包含实体和方法。

### <a name="entities"></a>实体
 实体描述字段的集合。 例如，实体可以表示在数据库中的表。 实体将显示为在 SharePoint 中的外部内容类型。 有关外部内容类型的详细信息，请参阅[外部内容类型是什么？](http://go.microsoft.com/fwlink/?LinkId=169293)

### <a name="methods"></a>方法
 要执行的操作对实体的字段的外部内容类型的使用者可以使用方法。 Updater 方法可能会使用户能够更改的地址和出生日期客户等位置`Address`并`BirthDate`是字段的`Customer`实体。

 Visual Studio 生成您的模型中的每个实体服务代码文件。 当将方法添加到您的模型时，Visual Studio 将生成服务代码文件中的相应方法。 将代码添加到每个方法来执行相应的任务。 例如，如果向模型添加 Creator 方法，Visual Studio 在你的服务代码文件中生成的创建者方法。 在用户单击时，调用此方法由 BDC 服务**新项**基于模型的列表中的按钮。 因此，将代码添加到将新数据添加到数据源的创建者方法。 有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)|演示如何创建新的模型或导入从 SharePoint 导出模型。|
|[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)|介绍如何使用 Visual Studio 设计工具设计模型的元素。|
|[何时使用 SharePoint Designer vs。Visual Studio 生成解决方案时使用 BCS](http://go.microsoft.com/fwlink/?LinkID=183448)|帮助您决定是使用 Visual Studio 还是使用 SharePoint Designer 来创建 BDC 模型。|
