---
title: 将快捷菜单项添加到 SharePoint 项目项扩展
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8041f9cbf19d1e1324478b92d2655f1377102b81
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401643"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension"></a>如何：将快捷菜单项添加到 SharePoint 项目项扩展
  通过使用项目项扩展，可以将快捷菜单项添加到现有 SharePoint 项目项。 用户右键单击中的项目项时出现的菜单项**解决方案资源管理器**。

 以下步骤假定已创建项目项扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

### <a name="to-add-a-shortcut-menu-item-in-a-project-item-extension"></a>若要在项目项扩展中添加快捷菜单项

1. 在<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A>方法将<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>实现、 句柄<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested>的事件*projectItemType*参数。

2. 在事件处理程序中的<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested>事件，添加一个新<xref:Microsoft.VisualStudio.SharePoint.IMenuItem>对象传递给<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A>或<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A>事件自变量参数的集合。

3. 在中<xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click>新的事件处理程序<xref:Microsoft.VisualStudio.SharePoint.IMenuItem>对象中，执行你想要在用户单击快捷菜单项时执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将快捷菜单项添加到事件接收器项目项。 当用户右键单击项目项中的**解决方案资源管理器**，然后单击**将消息写入到输出窗口**菜单项，Visual Studio 将显示一条消息中的**输出**窗口。

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionmenu.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#1](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionmenu.cs#1)]

 此示例使用 SharePoint 项目服务将写入到消息**输出**窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集的类库项目：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：将属性添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
