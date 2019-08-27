---
title: 扩展 SharePoint 项目项 |Microsoft Docs
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
ms.openlocfilehash: f60c95418379399196c461e055645ae7c85a473e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967391"
---
# <a name="extend-sharepoint-project-items"></a>扩展 SharePoint 项目项
  创建项目项扩展，如果想要将功能添加到已安装 Visual Studio 中的 SharePoint 项目项的类型。 例如，可以创建扩展的内置**事件接收器**或**列表定义**项目项在 Visual Studio 中，也可以创建自定义项目项类型的扩展。 此外可以创建适用于所有类型的 SharePoint 项目项的扩展。

## <a name="tasks-for-extending-sharepoint-project-items"></a>扩展 SharePoint 项目项的任务
 若要扩展的项目项，生成的 Visual Studio 扩展程序集实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>接口。 有关详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

 项目项扩展时，还可以对项目项添加了以下功能：

- 将快捷菜单项添加到项目项。 打开中的项目项的快捷菜单时显示的菜单项**解决方案资源管理器**。 通过右键单击项目项或选择它，然后选择打开快捷菜单**Shift**+**F10**密钥。 有关详细信息，请参阅[如何：将快捷菜单项添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)。

- 将自定义属性添加到项目项。 属性将出现在**属性**窗口中选择中的项目项时**解决方案资源管理器**。 有关详细信息，请参阅[如何：将属性添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)。

  有关演示如何创建、 部署和测试项目项扩展的演练，请参阅[演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)。

## <a name="understand-the-relationship-between-project-item-extensions-and-project-item-instances"></a>了解项目项扩展和项目项实例之间的关系
 在创建项目项扩展，Visual Studio 将加载您的扩展插件关联的类型的项目项添加到 SharePoint 项目时。 例如，如果创建的扩展**事件接收器**项目项，当用户将添加 Visual Studio 加载你的扩展**事件接收器**项目项的项目。 Visual Studio 使用您的扩展插件的同一个实例关联的项目项类型的所有实例。 在上一示例中，如果用户将添加第二个**事件接收器**项目到项目的项，您的扩展插件的同一个实例使用自定义第二个项目项。

 若要访问要扩展的项目项类型的特定实例，请处理之一<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents>的事件*projectItemType*参数的实现中<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A>方法。 例如，若要确定要扩展的类型的项目项添加到项目时，处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded>事件。 有关详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

## <a name="identifiers-for-sharepoint-project-items"></a>SharePoint 项目项的标识符
 每个 SharePoint 项目项都有相应的字符串标识符。 如果你想要执行以下任务，您必须知道项目项的标识符：

- 创建项目项的扩展。 在这种情况下，必须将想要扩展的构造函数的项目项的标识符传递<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>。 若要为所有项目项类型，请创建一个扩展，将传递 **\\** * 的字符串值。

- 以编程方式向项目添加项目项。 在这种情况下，必须将传递到的项目项的标识符<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemCollection.Add%2A>方法。

  下表列出了 Visual Studio 附带的 SharePoint 项目项的标识符。

|项目项名称|字符串标识符|
|-----------------------|-----------------------|
|业务数据目录模型|Microsoft.VisualStudio.SharePoint.BusinessDataConnectivity|
|内容类型|Microsoft.VisualStudio.SharePoint.ContentType|
|事件接收器|Microsoft.VisualStudio.SharePoint.EventHandler|
|空元素|Microsoft.VisualStudio.SharePoint.GenericElement|
|列表定义<br /><br /> 中的内容类型的列表定义|Microsoft.VisualStudio.SharePoint.ListDefinition|
|列表实例|Microsoft.VisualStudio.SharePoint.ListInstance|
|模块|Microsoft.VisualStudio.SharePoint.Module|
|顺序工作流<br /><br /> 状态机工作流|Microsoft.VisualStudio.SharePoint.Workflow|
|站点定义|Microsoft.VisualStudio.SharePoint.SiteDefinition|
|可视 Web 部件|Microsoft.VisualStudio.SharePoint.VisualWebPart|
|Web 部件|Microsoft.VisualStudio.SharePoint.WebPart|
|工作流关联窗体|Microsoft.VisualStudio.SharePoint.WorkflowAssociation|

## <a name="see-also"></a>请参阅
- [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：将快捷菜单项添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [如何：将属性添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
