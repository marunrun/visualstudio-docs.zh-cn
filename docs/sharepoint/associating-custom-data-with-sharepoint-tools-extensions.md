---
title: 将自定义数据相关联的 SharePoint 工具扩展 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], associating custom data
- project items [SharePoint development in Visual Studio], associating custom data
- SharePoint project items, associating custom data
- SharePoint projects, associating custom data
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9a2c1869791b250fb90c6a634f057797f3c57a62
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62987977"
---
# <a name="associate-custom-data-with-sharepoint-tools-extensions"></a>将自定义数据与 SharePoint 工具扩展相关联
  可以将自定义数据添加到 SharePoint 工具扩展中的某些对象。 如果你想要从您的扩展插件中的其他代码访问更高版本的扩展的一个部分中具有的数据，这很有用。 而不是实现自定义的方式来存储和访问数据，可以将数据与对象相关联在您的扩展插件，然后稍后从该对象检索该数据。

 将自定义数据添加到对象时，还想要保留在 Visual Studio 中的特定项相关的数据。 只需在 Visual Studio 中，因此您的扩展插件可能使用多个不同项后加载 SharePoint 工具扩展 (如项目、 项目项，或**服务器资源管理器**节点) 在任何时间。 如果必须只与特定项相关的自定义数据，您可以将数据添加到该对象表示的项。

 当将自定义数据添加到 SharePoint 工具扩展中的对象时，则不会保留数据。 该对象的生存期内仅有可用的数据。 垃圾回收功能回收对象后，会丢失数据。

 在扩展的 SharePoint 项目系统中，您还可以保存扩展是卸载操作后仍存在的字符串数据。 有关详细信息，请参阅[将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

## <a name="objects-that-can-contain-custom-data"></a>可以包含自定义数据的对象
 可以将自定义数据添加到实现 SharePoint 工具对象模型中的任何对象<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject>接口。 此接口定义只是一个属性， <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>，它是自定义数据对象的集合。 以下类型实现<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject>:

- <xref:Microsoft.VisualStudio.SharePoint.IMappedFolder>

- <xref:Microsoft.VisualStudio.SharePoint.IMenuItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectMember>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>

- <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentContext>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition>

## <a name="add-and-retrieve-custom-data"></a>添加和检索自定义数据
 若要将自定义数据添加到 SharePoint 工具扩展中的对象，获取<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>你想要向其中添加数据，然后使用该对象的属性<xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A>方法将数据添加到该对象。

 若要从 SharePoint 工具扩展中的对象中检索自定义数据，获取<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>属性的对象，然后使用以下方法之一：

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>。 此方法返回 **，则返回 true**数据对象存在，或**false**如果不存在。 此方法可用于检索值类型或引用类型的实例。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>。 此方法返回的数据对象，如果退出，或**null**如果不存在。 可以使用此方法检索引用类型的实例。

  下面的代码示例确定某个特定数据对象是否已与项目项相关联。 如果数据对象是不与项目项关联，则该代码将添加到对象<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>项目项的属性。 若要查看此上下文中的一个更大示例的示例，请参阅[如何：将属性添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#13)]
  [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#13)]

## <a name="see-also"></a>请参阅
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [如何：将属性添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
