---
title: 将自定义数据与 SharePoint 工具扩展相关联 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62987977"
---
# <a name="associate-custom-data-with-sharepoint-tools-extensions"></a>将自定义数据与 SharePoint 工具扩展相关联
  您可以将自定义数据添加到 SharePoint 工具扩展中的某些对象。 当你在扩展中的一个部分中包含要从扩展中的其他代码访问的数据时，这非常有用。 您可以将数据与扩展中的对象关联起来，然后在以后从同一对象中检索数据，而不是实现自定义方法来存储和访问数据。

 如果要保留与 Visual Studio 中特定项相关的数据，则将自定义数据添加到对象中也很有用。 SharePoint 工具扩展只在 Visual Studio 中加载一次，因此，您的扩展可以随时处理多个不同项 (如项目、项目项或 **服务器资源管理器**) 节点。 如果你的自定义数据仅与特定项相关，则可以将数据添加到表示该项的对象。

 将自定义数据添加到 SharePoint 工具扩展中的对象时，数据不会持久保存。 数据仅在该对象的生存期内可用。 通过垃圾回收来回收对象后，数据将丢失。

 在 SharePoint 项目系统的扩展中，还可以保存在卸载扩展后保留的字符串数据。 有关详细信息，请参阅 [在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

## <a name="objects-that-can-contain-custom-data"></a>可以包含自定义数据的对象
 您可以向实现接口的 SharePoint 工具对象模型中的任何对象添加自定义数据 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> 。 此接口仅定义一个属性， <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 该属性是自定义数据对象的集合。 以下类型实现 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> ：

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
 若要将自定义数据添加到 SharePoint 工具扩展中的对象，请获取要向其中 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 添加数据的对象的属性，然后使用 <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A> 方法将数据添加到对象。

 若要从 SharePoint 工具扩展中的对象检索自定义数据，请获取该 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 对象的属性，然后使用以下方法之一：

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>. 如果该数据对象存在，则此方法返回 **true** ; 如果该对象不存在，则返回 **false** 。 您可以使用此方法检索值类型或引用类型的实例。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>. 如果数据对象退出，此方法将返回该对象; 如果该对象不存在，则返回 **null** 。 您只能使用此方法来检索引用类型的实例。

  下面的代码示例确定某个数据对象是否已与项目项关联。 如果数据对象尚未与项目项关联，则代码会将对象添加到 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 项目项的属性。 若要在更大的示例上下文中查看此示例，请参阅 [如何：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#13)]
  [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#13)]

## <a name="see-also"></a>另请参阅
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [如何：向 SharePoint 项目添加属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [如何：向自定义 SharePoint 项目项类型添加属性](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
