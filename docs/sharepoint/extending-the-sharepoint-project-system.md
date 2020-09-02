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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62557019"
---
# <a name="extend-the-sharepoint-project-system"></a>扩展 SharePoint 项目系统
  可以通过在 Visual Studio 中使用一组项目模板和项模板来创建 SharePoint 解决方案。 这些模板满足许多开发方案的要求，但您可能会发现某些情况下不提供您需要的功能。 在这些情况下，您可以扩展 SharePoint 项目系统。

## <a name="overview-of-the-sharepoint-project-system"></a>SharePoint 项目系统概述
 SharePoint 项目系统基于 *sharepoint 项目项*的基本组件。 SharePoint 项目项表示单个 SharePoint 自定义项，例如列表定义、Web 部件或内容类型。

 SharePoint 项目是一个 Visual Studio 项目，其中包含一个或多个 SharePoint 项目项。 SharePoint 项目还包含其他组件，这些组件定义如何将项目项分组为功能和包以进行部署。

 有关 SharePoint 项目项和 SharePoint 项目的内容的详细信息，请参阅 [为 sharepoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

## <a name="how-to-extend-the-sharepoint-project-system"></a>如何扩展 SharePoint 项目系统
 可以通过以下方式扩展 SharePoint 项目系统：

- 定义自己的 SharePoint 项目项类型，并将其与 Visual Studio 中的新项模板或项目模板关联。 例如，你可以定义一个用于创建自定义操作或字段的 SharePoint 项目项类型。 有关详细信息，请参阅 [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)。

- 扩展已安装在 Visual Studio 中的 SharePoint 项目项类型。 例如，可以将快捷菜单项添加到 **解决方案资源管理器** 中的项目项，并在开发人员选择菜单项时自定义项目项。 有关详细信息，请参阅 [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

- 扩展 SharePoint 项目。 例如，你可以添加事件处理程序，以便在 SharePoint 项目中添加或删除项时执行特定任务。 有关详细信息，请参阅 [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)。

- 扩展 SharePoint 项目项和 SharePoint 项目的打包和部署行为。 例如，你可以创建自己的部署步骤，以在部署或收回项目时执行，或者在 Visual Studio 执行某些部署步骤时执行其他自定义任务。 有关详细信息，请参阅 [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

## <a name="common-development-tasks"></a>常见开发任务
 您可以在 SharePoint 项目系统的扩展中执行以下常见任务：

- 用项目项和多种不同类型的项目文件保存自定义字符串数据。 有关详细信息，请参阅 [在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

- 将 SharePoint 项目系统中的对象转换为 Visual Studio 自动化对象模型或集成对象模型中的相应对象，反之亦然。 有关详细信息，请参阅 [SharePoint 项目系统类型和其他 Visual Studio 项目类型之间的将](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)。

## <a name="see-also"></a>另请参阅
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [在 SharePoint 项目系统类型和其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
