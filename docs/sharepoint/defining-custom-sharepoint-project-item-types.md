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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580779"
---
# <a name="define-custom-sharepoint-project-item-types"></a>定义自定义 SharePoint 项目项类型
  若要创建新类型的 SharePoint 项目项，请定义新的 SharePoint 项目项类型。 例如，Visual Studio 不包括用于将字段或自定义操作添加到 SharePoint 站点的 SharePoint 项目项。 您可以定义自己的 SharePoint 项目项类型，以便创建字段、自定义操作或其他类型的 SharePoint 组件。

## <a name="tasks-for-defining-sharepoint-project-item-types"></a>用于定义 SharePoint 项目项类型的任务
 若要定义自定义项目项类型，请生成用于实现接口的 Visual Studio 扩展程序集 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 。 有关详细信息，请参阅 [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

 定义自定义项目项类型时，还可以将以下功能添加到项目项：

- 向项目项添加快捷菜单项。 在**解决方案资源管理器**中打开项目项的快捷菜单时，将显示该菜单项，方法是右键单击项目项，或通过选择该项目，然后选择**Shift** + **F10**键。 有关详细信息，请参阅 [如何：将快捷菜单项添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)。

- 向项目项添加自定义属性。 在**解决方案资源管理器**中选择项目项时，属性将显示在 "**属性**" 窗口中。 有关详细信息，请参阅 [如何：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  若要使其他开发人员能够在 Visual Studio 中使用您的项目项，请创建一个 spdata 文件并创建与该项目项关联的项模板或项目模板。 有关详细信息，请参阅 [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

## <a name="understand-the-relationship-between-project-item-types-and-project-item-instances"></a>了解项目项类型和项目项实例之间的关系
 定义 SharePoint 项目项类型时，当关联类型的项目项添加到 SharePoint 项目时，Visual Studio 将加载您的扩展。 例如，如果定义了一个新的 **自定义操作** 项目项类型，则当用户向项目添加 **自定义操作** 项目项时，Visual Studio 将加载你的扩展。 对于关联的项目项类型的所有实例，Visual Studio 均使用您的扩展的相同实例。 在上面的示例中，如果用户向项目中添加了第二个 **自定义操作** 项目项，则将使用扩展的同一个实例自定义第二个项目项。

 若要访问项目项类型的特定实例，请 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 在方法的实现中处理 *projectItemTypeDefinition* 参数的一个事件 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 。 例如，若要确定自定义类型的项目项何时添加到项目中，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 事件。 有关详细信息，请参阅 [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

## <a name="see-also"></a>另请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：向自定义 SharePoint 项目项类型添加属性](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [如何：向自定义 SharePoint 项目项类型添加快捷菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项模板创建自定义操作项目项（第2部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
