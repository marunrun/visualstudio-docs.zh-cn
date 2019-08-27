---
title: 将属性添加到自定义 SharePoint 项目项类型
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
ms.openlocfilehash: 4d44f4d5995be8bacc447ea3f915663a309bee77
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401654"
---
# <a name="how-to-add-a-property-to-a-custom-sharepoint-project-item-type"></a>如何：将属性添加到自定义的 SharePoint 项目项类型
  在定义的自定义 SharePoint 项目项类型时，您可以向项目项添加属性。 属性将出现在**属性**窗口中选择项目项时**解决方案资源管理器**。

 以下步骤假定你已定义 SharePoint 项目项类型。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

### <a name="to-add-a-property-to-a-definition-of-a-project-item-type"></a>若要将属性添加到项目项类型定义

1. 定义具有表示要添加到自定义项目项类型的属性的公共属性的类。 如果你想要将多个属性添加到自定义项目项类型，您可以在同一个类或不同的类中定义所有属性。

2. 在<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>方法将<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>实现、 句柄<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested>的事件*projectItemTypeDefinition*参数。

3. 中的事件处理程序<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested>事件，添加到您的自定义属性的类的实例<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A>事件自变量参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何添加名为的属性**的示例属性**向自定义项目项类型。

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#11](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#11)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#11](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#11)]

### <a name="understand-the-code"></a>理解代码
 若要确保在同一个实例`CustomProperties`每次使用类<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested>事件发生时，代码示例将保存到的属性对象<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>属性会发生此事件的项目项第一个时间。 再次发生此事件时，代码将检索此对象。 有关使用详细信息<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>属性将数据保存与项目项，请参阅[关联自定义数据与 SharePoint 工具扩展](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 保存属性值，更改**设置**访问器`ExampleProperty`将保存到的新值<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>属性<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>属性关联的对象。 有关使用详细信息<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>属性以使用项目项将数据保存请参阅[将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以定义自定义属性的显示方式和行为**属性**通过应用中的属性窗口<xref:System.ComponentModel>到属性定义的命名空间。 以下属性可在许多情况下：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定将出现在属性的名称**属性**窗口。

- <xref:System.ComponentModel.DescriptionAttribute>：指定显示的说明字符串中的底部**属性**窗口时选择了该属性。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在显示的字符串之间的自定义转换**属性**窗口和一个非字符串属性值。

- <xref:System.ComponentModel.EditorAttribute>：指定要用于修改属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 这些代码示例需要引用以下程序集的类库项目：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要启用其他开发人员能够使用您的项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署的项目项，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集、 模板和你想要将与项目项一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
