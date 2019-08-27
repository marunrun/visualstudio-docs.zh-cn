---
title: 扩展 SharePoint 项目系统 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending projects
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7dce10c2bc44eb4fde6a6e38417d136ea5e9ba41
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62557019"
---
# <a name="extend-the-sharepoint-project-system"></a>扩展 SharePoint 项目系统
  可以通过使用 Visual Studio 中的一组项目模板和项模板创建 SharePoint 解决方案。 这些模板满足要求的许多开发方案，但您可能会发现某些情况下，它们不提供所需的功能。 在这些情况下，可以扩展 SharePoint 项目系统。

## <a name="overview-of-the-sharepoint-project-system"></a>SharePoint 项目系统的概述
 SharePoint 项目系统为基础的基本组成部分*SharePoint 项目项*。 SharePoint 项目项表示单个的 SharePoint 自定义，如列表定义、 Web 部件或内容类型。

 SharePoint 项目是 Visual Studio 项目包含一个或多个 SharePoint 项目项。 SharePoint 项目还包含定义如何将项目项分组为功能和部署的包的其他组件。

 SharePoint 项目项和 SharePoint 项目的内容的详细信息，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

## <a name="how-to-extend-the-sharepoint-project-system"></a>如何扩展 SharePoint 项目系统
 你可以按以下方式扩展 SharePoint 项目系统：

- 定义你自己的 SharePoint 项目项类型并将其与新项模板或 Visual Studio 中的项目模板关联。 例如，您可以创建自定义操作或字段的定义 SharePoint 项目项类型。 有关详细信息，请参阅[定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)。

- 扩展已安装 Visual Studio 中的 SharePoint 项目项类型。 例如，可以将快捷菜单项添加到项目项中**解决方案资源管理器**和开发人员选择菜单项时自定义项目项。 有关详细信息，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

- 扩展 SharePoint 项目。 例如，可以添加事件处理程序时添加或删除从 SharePoint 项目项执行特定任务。 有关详细信息，请参阅[扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)。

- 扩展 SharePoint 项目项和 SharePoint 项目的打包和部署行为。 例如，可以创建自己的部署步骤来部署或收回一个项目，或当 Visual Studio 执行某些部署步骤时，你可以执行其他自定义任务时执行。 有关详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

## <a name="common-development-tasks"></a>常见开发任务
 扩展 SharePoint 项目系统中，可以执行以下常见任务：

- 将自定义字符串数据保存在多种不同类型的项目文件、 项目项。 有关详细信息，请参阅[将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

- 将对象转换到 Visual Studio 自动化对象模型或集成对象模型中的相应对象在 SharePoint 项目系统中，反之亦然。 有关详细信息，请参阅[SharePoint 项目系统类型和其他 Visual Studio 项目类型之间将](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)。

## <a name="see-also"></a>请参阅
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [SharePoint 项目系统类型与其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
