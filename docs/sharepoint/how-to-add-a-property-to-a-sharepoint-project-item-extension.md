---
title: 如何：向 SharePoint 项目项扩展添加属性 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 337536d2219ce8494f96769bc79f10967883e61a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015980"
---
# <a name="how-to-add-a-property-to-a-sharepoint-project-item-extension"></a>如何：向 SharePoint 项目项扩展添加属性
  可以使用项目项扩展将属性添加到已在 Visual Studio 中安装的任何 SharePoint 项目项。 在**解决方案资源管理器**中选择项目项时，属性将显示在 "**属性**" 窗口中。

 以下步骤假设已创建项目项扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

### <a name="to-add-a-property-to-a-project-item-extension"></a>向项目项扩展添加属性

1. 使用公共属性定义一个类，该类表示要添加到项目项类型的属性。 如果要将多个属性添加到项目项类型，则可以在同一类或不同类中定义所有属性。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 实现的方法中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> ，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> *projectItemType*参数的事件。

3. 在事件的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> ，将 properties 类的实例添加到 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> 事件参数参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何将名为**Example 属性**的属性添加到事件接收器项目项。

 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionproperty.cs#8)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionproperty.vb#8)]

### <a name="understand-the-code"></a>了解代码
 若要确保 `CustomProperties` 每次事件发生时使用类的同一个实例 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> ，则在第一次发生此事件时，该代码示例会将 properties 对象添加到 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 项目项的属性。 每当再次发生此事件时，代码就会检索此对象。 有关使用 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性将数据与项目项关联的详细信息，请参阅[将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 若要将更改保存到属性值，则的**set**访问器用于将 `ExampleProperty` 新值保存到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> 与属性关联的对象的属性。 若要详细了解如何使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> 属性来保存带有项目项的数据，请参阅[在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 通过将命名空间中的特性应用于属性定义，可以定义自定义属性在 "**属性**" 窗口中的显示方式和行为方式 <xref:System.ComponentModel> 。 以下属性在许多情况下都很有用：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定在 "**属性**" 窗口中显示的属性的名称。

- <xref:System.ComponentModel.DescriptionAttribute>：指定在选择属性时在 "**属性**" 窗口底部显示的描述字符串。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在 "**属性**" 窗口中显示的字符串与非字符串属性值之间的自定义转换。

- <xref:System.ComponentModel.EditorAttribute>：指定用于修改属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 这些示例需要一个类库项目，其中包含对以下程序集的引用：

- VisualStudio

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展（VSIX）包，并为要使用该扩展分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：向 SharePoint 项目项扩展添加快捷菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
