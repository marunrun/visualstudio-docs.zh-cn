---
title: 扩展 SharePoint 项目 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6bc92d65ed179c7f2cb2f569a7d254a025887845
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967476"
---
# <a name="extend-sharepoint-projects"></a>扩展 SharePoint 项目
  如果想要自定义 SharePoint 项目的项目级功能，请创建一个项目扩展。 例如，可以添加自定义项目属性中，或对用户开发 Visual Studio 中的 SharePoint 解决方案时引发的项目级事件做出响应。

## <a name="create-project-extensions"></a>创建项目扩展
 若要扩展的项目项，生成的 Visual Studio 扩展程序集实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>接口。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

 在创建项目扩展时，还可以向 SharePoint 项目添加了以下功能：

- 添加快捷菜单项。 打开中的 SharePoint 项目节点的快捷菜单时显示的菜单项**解决方案资源管理器**通过右键单击节点或选择它，然后选择**Shift** + **F10**密钥。 有关详细信息，请参阅[如何：将快捷菜单项添加到 SharePoint 项目](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)。

- 添加自定义属性。 属性将出现在**属性**窗口中选择的 SharePoint 项目中时**解决方案资源管理器**。 有关详细信息，请参阅[如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

  有关演示如何创建、 部署和测试项目扩展的演练，请参阅[演练：创建 SharePoint 项目扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)。

## <a name="understand-the-relationship-between-project-extensions-and-project-instances"></a>了解项目扩展和项目实例之间的关系
 该扩展时创建的项目扩展，请加载任何类型的 SharePoint 项目中打开时[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 包含多个 SharePoint 项目模板，如列表定义、 内容类型和事件接收器。 但是，没有一个 SharePoint 项目类型。 在显示的项目类型**新的项目**对话框是捆绑在一起的一个或多个 SharePoint 项目项的模板。 由于只有一个 SharePoint 项目类型，扩展为一个项目创建适用于所有 SharePoint 项目。 例如，不能请创建一个扩展，仅适用于**内容类型**项目。

 若要访问特定项目实例，请处理之一<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents>的事件*projectService*参数的实现中<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A>方法。 例如，若要确定 SharePoint 项目添加到解决方案时，处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded>事件。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

## <a name="see-also"></a>请参阅
- [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：将快捷菜单项添加到 SharePoint 项目](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [演练：创建 SharePoint 项目扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
