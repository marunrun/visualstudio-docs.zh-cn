---
title: 如何：向 SharePoint 项目添加属性 |Microsoft Docs
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
ms.openlocfilehash: eb72b0546b504e2df1a7e93ea9d4def350143d1d
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015927"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>如何：向 SharePoint 项目添加属性
  可以使用项目扩展将属性添加到任何 SharePoint 项目。 在**解决方案资源管理器**中选择项目时，属性将显示在 "**属性**" 窗口中。

 以下步骤假设已创建项目扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

### <a name="to-add-a-property-to-a-sharepoint-project"></a>将属性添加到 SharePoint 项目

1. 使用公共属性定义一个类，该类表示要添加到 SharePoint 项目中的属性。 如果要添加多个属性，可以在同一个类或不同的类中定义所有属性。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 实现的方法中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> *projectService*参数的事件。

3. 在事件的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> ，将 properties 类的实例添加到 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A> 事件参数参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何将两个属性添加到 SharePoint 项目。 一个属性在项目用户选项文件（ *.csproj. 用户*文件或 *.vbproj*文件）中保留其数据。 其他属性在项目文件（*.csproj*文件或 *.vbproj*文件）中保留其数据。

 [!code-vb[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#1)]
 [!code-csharp[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#1)]

### <a name="understand-the-code"></a>了解代码
 若要确保 `CustomProjectProperties` 每次事件发生时使用类的同一个实例 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> ，则在 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 第一次发生此事件时，该代码示例会将 properties 对象添加到项目的属性。 每当再次发生此事件时，代码就会检索此对象。 有关使用 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性将数据与项目相关联的详细信息，请参阅[将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 若要将更改保存到属性值，属性的**set**访问器使用以下 api：

- `CustomUserFileProperty`使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> 属性将其值保存到项目用户选项文件中。

- `CustomProjectFileProperty`使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> 方法将其值保存到项目文件。

  有关保留这些文件中的数据的详细信息，请参阅在[SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 通过将命名空间中的特性应用于属性定义，可以定义自定义属性在 "**属性**" 窗口中的显示方式和行为方式 <xref:System.ComponentModel> 。 以下属性在许多情况下都很有用：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定在 "**属性**" 窗口中显示的属性的名称。

- <xref:System.ComponentModel.DescriptionAttribute>：指定在选择属性时在 "**属性**" 窗口底部显示的描述字符串。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在 "**属性**" 窗口中显示的字符串与非字符串属性值之间的自定义转换。

- <xref:System.ComponentModel.EditorAttribute>：指定用于修改属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio

- VisualStudio

- VisualStudio。

- VisualStudio.. 8。0

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展（VSIX）包，并为要使用该扩展分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：向 SharePoint 项目添加快捷菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
