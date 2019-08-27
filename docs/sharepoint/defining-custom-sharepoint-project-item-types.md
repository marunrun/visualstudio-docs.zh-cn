---
title: 定义自定义 SharePoint 项目项类型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e5f32abba4c4cbdeab59ed66e38019d913e704e6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62580779"
---
# <a name="define-custom-sharepoint-project-item-types"></a>定义自定义 SharePoint 项目项类型
  当你想要创建一种新的 SharePoint 项目项时，请定义新的 SharePoint 项目项类型。 例如，Visual Studio 不包括添加字段或自定义操作向 SharePoint 站点的 SharePoint 项目项。 可以定义自己的用于创建字段、 自定义操作或其他类型的 SharePoint 组件的 SharePoint 项目项的类型。

## <a name="tasks-for-defining-sharepoint-project-item-types"></a>用于定义 SharePoint 项目项类型的任务
 若要定义的自定义项目项类型，生成的 Visual Studio 扩展程序集实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>接口。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

 在定义的自定义项目项类型时，还可以对项目项添加了以下功能：

- 将快捷菜单项添加到项目项。 打开中的项目项的快捷菜单时显示的菜单项**解决方案资源管理器**右键单击项目项，或选择它，然后选择**Shift** + **F10**密钥。 有关详细信息，请参阅[如何：将快捷菜单项添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)。

- 将自定义属性添加到项目项。 属性将出现在**属性**窗口中选择中的项目项时**解决方案资源管理器**。 有关详细信息，请参阅[如何：将属性添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  若要启用其他开发人员在 Visual Studio 中使用您的项目项，请创建.spdata 文件并创建项模板或与项目项关联的项目模板。 有关详细信息，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

## <a name="understand-the-relationship-between-project-item-types-and-project-item-instances"></a>了解项目项类型和项目项实例之间的关系
 在定义 SharePoint 项目项类型时，Visual Studio 将加载您的扩展插件关联的类型的项目项添加到 SharePoint 项目时。 例如，如果你定义一个新**自定义操作**项目项类型、 用户添加时，Visual Studio 将加载你的扩展**自定义操作**项目项的项目。 Visual Studio 使用您的扩展插件的同一个实例关联的项目项类型的所有实例。 在上一示例中，如果用户将添加第二个**自定义操作**项目到项目的项，您的扩展插件的同一个实例使用自定义第二个项目项。

 若要访问你的项目项类型的特定实例，请处理之一<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents>的事件*projectItemTypeDefinition*参数的实现中<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>方法。 例如，若要确定你自定义类型的项目项添加到项目时，处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded>事件。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

## <a name="see-also"></a>请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将属性添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [创建项模板和用于 SharePoint 项目项的项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [部署 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
