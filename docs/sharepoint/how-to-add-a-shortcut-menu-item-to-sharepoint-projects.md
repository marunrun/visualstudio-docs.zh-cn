---
title: 如何：将快捷菜单项添加到 SharePoint 项目 |Microsoft Docs
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
ms.openlocfilehash: 5b5db3fe3aaf8dc57c7df6a63810106ae9fb30fb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967117"
---
# <a name="how-to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>如何：将快捷菜单项添加到 SharePoint 项目
  可以将快捷菜单项添加到任何 SharePoint 项目。 用户右键单击项目节点中的时出现的菜单项**解决方案资源管理器**。

 以下步骤假定你已创建了一个项目扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

### <a name="to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>若要将快捷菜单项添加到 SharePoint 项目

1. 在<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A>方法将<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>实现、 句柄<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested>的事件*projectService*参数。

2. 在事件处理程序中的<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested>事件，添加一个新<xref:Microsoft.VisualStudio.SharePoint.IMenuItem>对象传递给<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.ActionMenuItems%2A>或<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.AddMenuItems%2A>事件自变量参数的集合。

3. 在中<xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click>新的事件处理程序<xref:Microsoft.VisualStudio.SharePoint.IMenuItem>对象中，执行你想要在用户单击快捷菜单项时执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将快捷菜单项添加到 SharePoint 中的项目节点**解决方案资源管理器**。 当用户右键单击项目节点，然后单击**将消息写入到输出窗口**菜单项，Visual Studio 将显示中的消息**输出**窗口。 此示例中使用 SharePoint 项目服务来显示消息。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

 [!code-csharp[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs#1)]
 [!code-vb[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集的类库项目：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
