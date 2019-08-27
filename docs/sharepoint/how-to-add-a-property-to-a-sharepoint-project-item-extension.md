---
title: 如何：将属性添加到 SharePoint 项目项扩展 |Microsoft Docs
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
ms.openlocfilehash: 20a7abaa8c132b3cd1679ab95ed8154b8ca86502
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967222"
---
# <a name="how-to-add-a-property-to-a-sharepoint-project-item-extension"></a>如何：将属性添加到 SharePoint 项目项扩展
  项目项扩展可用于将属性添加到任何已安装 Visual Studio 中的 SharePoint 项目项。 属性将出现在**属性**窗口中选择项目项时**解决方案资源管理器**。

 以下步骤假定已创建项目项扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

### <a name="to-add-a-property-to-a-project-item-extension"></a>若要将属性添加到项目项扩展

1. 定义具有表示要添加到项目项类型的属性的公共属性的类。 如果你想要将多个属性添加到项目项类型，您可以在同一个类或不同的类中定义所有属性。

2. 在<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A>方法将<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>实现、 句柄<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested>的事件*projectItemType*参数。

3. 中的事件处理程序<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested>事件，将添加到你属性类的实例<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A>事件自变量参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何添加名为的属性**的示例属性**到事件接收器项目项。

 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionproperty.cs#8)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionproperty.vb#8)]

### <a name="understand-the-code"></a>理解代码
 若要确保在同一个实例`CustomProperties`每次使用类<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested>事件发生时，代码示例将添加到的属性对象<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>属性会发生此事件的项目项第一个时间。 再次发生此事件时，代码将检索此对象。 有关使用详细信息<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>请参阅将数据与项目项关联的属性[关联自定义数据与 SharePoint 工具扩展](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 保存属性值，更改**设置**访问器`ExampleProperty`将保存到的新值<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>属性<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>属性关联的对象。 有关使用详细信息<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>属性以使用项目项将数据保存请参阅[将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以定义自定义属性的显示方式和行为**属性**通过应用中的属性窗口<xref:System.ComponentModel>到属性定义的命名空间。 以下属性可在许多情况下：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定将出现在属性的名称**属性**窗口。

- <xref:System.ComponentModel.DescriptionAttribute>：指定显示的说明字符串中的底部**属性**窗口时选择了该属性。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在显示的字符串之间的自定义转换**属性**窗口和一个非字符串属性值。

- <xref:System.ComponentModel.EditorAttribute>：指定要用于修改属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 这些示例需要引用以下程序集的类库项目：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：将快捷菜单项添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
