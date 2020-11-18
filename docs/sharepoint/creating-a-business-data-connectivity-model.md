---
title: 创建业务数据连接模型 |Microsoft Docs
description: 使用 Visual Studio 创建 (BDC) 模型的业务数据连接，或自定义现有 BDC 模型。 每个 SharePoint 项目只能包含一个模型。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 0486ce6ac53850b1b607f9e7f859806cdc3ef8fe
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850463"
---
# <a name="create-a-business-data-connectivity-model"></a>创建业务数据连接模型
  您可以使用 Visual Studio 创建 (BDC) 模型的业务数据连接，或自定义现有 BDC 模型。 每个 SharePoint 项目只能包含一个模型。 有关详细信息，请参阅将 [业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)。

## <a name="create-a-new-model"></a>创建新模型
 若要创建新模型，请创建 **业务数据连接模型** 项目或将 **业务数据连接模型** 项添加到 **空的 SharePoint 项目** 中。

> [!NOTE]
> 你必须已 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 在计算机上安装了。

 Visual Studio 将文件夹添加到项目。 此文件夹具有您在 "**添加新项**" 对话框中为 "**业务数据连接模型**" 项指定的名称。 如果创建新的 **业务数据连接模型** 项目，则 Visual Studio 会将该文件夹命名为 **BdcModel1**。

 Visual Studio 将以下文件添加到新文件夹：

|文件|说明|
|----------|-----------------|
|模型定义文件|包含用于定义实体、方法、业务线 (LOB) 系统对象和其他描述模型的元数据的 XML。<br /><br /> 使用 "BDC 设计器"、" **Bdc 资源管理器**"、" **Bdc 方法详细信息** " 窗口和 " **属性** " 窗口修改此文件中的元数据。|
|实体服务代码文件|包含检索、更新和删除默认实体的实例的方法。|

 若要定义实体的属性，请编辑实体代码文件。 有关详细信息，请参阅 [如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

 若要检索、更新和删除实体的实例，请将代码添加到实体服务代码文件中。 有关详细信息，请参阅 [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

 编译项目时，Visual Studio 将创建一个程序集。 确保不向项目中添加其他项（将代码添加到项目程序集） (例如： **顺序工作流** 项或) 的 **Web 部件** 项。 部署解决方案时，该项目的代码不会运行，因为解决方案包不会将程序集复制到全局程序集缓存中。  解决方案包仅将程序集部署到 SharePoint 中的 BDC 数据库。

> [!NOTE]
> 调试项目时，Visual Studio 会将程序集复制到本地计算机上的两个位置。

## <a name="add-an-existing-model"></a>添加现有模型
 您可以导入使用其他工具（如 SharePoint Designer）创建的模型。 在以下情况下，可以选择将现有模型导入项目：

- 自定义已部署到 SharePoint 服务器场的模型。

- 将现有模型打包并部署到多个 SharePoint 服务器场。

  在任一情况下，你导入的模型中定义的 LOB 系统都不会受到影响，并将继续按预期方式工作。 若要向 SharePoint 项目添加现有模型，请使用 Visual Studio 中的 " **添加现有项** " 对话框。 有关详细信息，请参阅 [如何：向 SharePoint 项目添加现有 BDC 模型文件](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)。

  可以通过在 **添加 .net 程序集 LobSystem** 中选择一个选项，将类型 .NET Framework 程序集类型的 LOB 系统添加到导入的模型中。 这使您可以编写自定义代码，并使用设计器为导入的模型定义元数据。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)|说明如何创建新的 BDC 模型。|
|[如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)|说明如何将现有模型导入 SharePoint 项目中。|
|[如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)|描述如何在 Web 部件或网页使用模型时，提供与模型元数据合并的字符串。|
|[如何：在 BDC 功能中包含自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)|演示如何在功能中包含自定义程序集。|
