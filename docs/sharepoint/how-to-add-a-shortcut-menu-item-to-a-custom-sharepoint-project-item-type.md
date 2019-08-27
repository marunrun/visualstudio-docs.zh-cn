---
title: 将快捷菜单项添加到自定义 SharePoint 项目项类型
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
ms.openlocfilehash: 95c47cdc00fc9035870aed4ac2e0bee4d3c1c5af
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401623"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type"></a>如何：将快捷菜单项添加到自定义的 SharePoint 项目项类型
  在定义的自定义 SharePoint 项目项类型时，可以将快捷菜单项添加到项目项。 用户右键单击中的项目项时出现的菜单项**解决方案资源管理器**。

 以下步骤假定你已定义 SharePoint 项目项类型。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

### <a name="to-add-a-shortcut-menu-item-to-a-custom-project-item-type"></a>若要将快捷菜单项添加到自定义项目项类型

1. 在<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>方法将<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>实现、 句柄<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested>的事件*projectItemTypeDefinition*参数。

2. 在事件处理程序中的<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested>事件，添加一个新<xref:Microsoft.VisualStudio.SharePoint.IMenuItem>对象传递给<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A>或<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A>事件自变量参数的集合。

3. 在中<xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click>新的事件处理程序<xref:Microsoft.VisualStudio.SharePoint.IMenuItem>对象中，执行你想要在用户选择快捷菜单项时执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将一个上下文菜单项添加到自定义项目项类型。 当用户打开从项目项的快捷菜单**解决方案资源管理器**，并选择**将消息写入到输出窗口**菜单项，Visual Studio 将显示一条消息中的**输出**窗口。

 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#4](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypemenu.cs#4)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#4](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypemenu.vb#4)]

 此示例使用 SharePoint 项目服务将写入到消息**输出**窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集的类库项目：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要启用其他开发人员能够使用您的项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署的项目项，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集、 模板和你想要将与项目项一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将属性添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
