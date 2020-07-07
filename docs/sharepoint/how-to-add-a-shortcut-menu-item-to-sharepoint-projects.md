---
title: 如何：向 SharePoint 项目添加快捷菜单项 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 4e43d8d7717302eb8ab250935188bc2db3bdd66a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014840"
---
# <a name="how-to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>如何：向 SharePoint 项目添加快捷菜单项
  您可以向任何 SharePoint 项目添加快捷菜单项。 当用户在**解决方案资源管理器**中右键单击项目节点时，将显示菜单项。

 以下步骤假设已创建项目扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

### <a name="to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>向 SharePoint 项目添加快捷菜单项

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 实现的方法中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> *projectService*参数的事件。

2. 在事件的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> ，向 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.ActionMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.AddMenuItems%2A> 事件参数参数的或集合添加一个新的对象。

3. 在 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> 新对象的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> ，执行用户单击快捷菜单项时要执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将快捷菜单项添加到**解决方案资源管理器**中的 SharePoint 项目节点。 当用户右键单击项目节点并单击 "**写入消息到输出窗口**" 菜单项时，Visual Studio 会在 "**输出**" 窗口中显示一条消息。 此示例使用 SharePoint 项目服务显示消息。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

 [!code-csharp[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs#1)]
 [!code-vb[SPExtensibility.ProjectExtension.Menu#1](../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，其中包含对以下程序集的引用：

- VisualStudio

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展（VSIX）包，并为要使用该扩展分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：向 SharePoint 项目添加属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
