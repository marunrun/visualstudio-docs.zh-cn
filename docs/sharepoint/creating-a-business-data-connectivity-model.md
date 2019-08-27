---
title: 创建业务数据连接模型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], model
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- SharePoint development in Visual Studio, Business Data Connectivity service
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9f3da13858507a3ff176aaa0a44051674fd5285f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443555"
---
# <a name="create-a-business-data-connectivity-model"></a>创建业务数据连接模型
  可以创建业务数据连接 (BDC) 模型，也可以使用 Visual Studio 自定义现有 BDC 模型。 每个 SharePoint 项目可以包含一个模型。 有关详细信息，请参阅[将业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)。

## <a name="create-a-new-model"></a>创建新的模型
 若要创建新模型，创建**业务数据连接模型**项目或添加**业务数据连接模型**项**空 SharePoint 项目**。

> [!NOTE]
> 您必须具有[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]在计算机上安装。

 Visual Studio 向项目添加一个文件夹。 此文件夹的名称为指定的名称**业务数据连接模型**中的项**添加新项**对话框。 如果您创建一个新**业务数据连接模型**项目，Visual Studio 将该文件夹命名**BdcModel1**。

 Visual Studio 将以下文件添加到新文件夹：

|文件|描述|
|----------|-----------------|
|模型定义文件|包含用于定义实体、 方法、 业务线 (LOB) 系统对象和其他元数据描述模型的 XML。<br /><br /> 使用 BDC 设计器中，修改此文件中的元数据**BDC 资源管理器**， **BDC 方法详细信息**窗口中，并且**属性**窗口。|
|实体服务代码文件|包含检索、 更新和删除的默认实体实例的方法。|

 若要定义实体的属性，请编辑实体的代码文件。 有关详细信息，请参阅[如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

 若要检索、 更新和删除实体的实例，请将代码添加到实体服务代码文件。 有关详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 在编译项目时，Visual Studio 创建程序集。 确保不要将其他项添加到将代码添加到项目程序集的项目 (例如：**顺序工作流**项或**Web 部件**项)。 因为解决方案包不会复制到全局程序集缓存程序集部署解决方案时，将不会运行该项目的代码。  解决方案包部署到仅在 SharePoint 中的 BDC 数据库程序集。

> [!NOTE]
> 调试项目时，visual Studio 将该程序集复制到本地计算机上的这两个位置。

## <a name="add-an-existing-model"></a>添加现有模型
 您可以导入已通过使用其他工具，例如 SharePoint 设计器的模型。 您可以选择现有模型导入在以下情况下你的项目：

- 若要自定义已部署到 SharePoint 服务器场的模型。

- 若要打包并部署到多个 SharePoint 服务器场的现有模型。

  在任一情况下，导入的模型中定义的 LOB 系统不会受到影响，并将继续按预期方式工作。 若要将现有模型添加到 SharePoint 项目，请使用 Visual Studio**添加现有项**对话框。 有关详细信息，请参阅[如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)。

  您可以通过选择中的一个选项添加到导入的模型类型的.NET Framework 程序集的 LOB 系统**添加.NET 程序集 LobSystem**。 这使你可以编写自定义代码和设计器用于定义导入模型的元数据。

## <a name="related-topics"></a>相关主题

|标题|说明|
|-----------|-----------------|
|[如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)|演示如何创建新的 BDC 模型。|
|[如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)|演示如何将现有模型导入 SharePoint 项目。|
|[如何：使用资源文件指定本地化的名称、 属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)|介绍如何提供模型元数据合并的字符串时该模型由 Web 部件或网页。|
|[如何：在 BDC 功能中包含自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)|演示如何在功能中引入的自定义程序集。|
