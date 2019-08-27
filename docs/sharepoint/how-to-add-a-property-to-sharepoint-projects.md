---
title: 如何：将属性添加到 SharePoint 项目 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: a6f1ecd427b1c715649bc2118be5ab384a74c585
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967209"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>如何：将属性添加到 SharePoint 项目
  项目扩展可用于将属性添加到任何 SharePoint 项目。 属性将出现在**属性**窗口中选择项目时**解决方案资源管理器**。

 以下步骤假定你已创建了一个项目扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

### <a name="to-add-a-property-to-a-sharepoint-project"></a>若要将属性添加到 SharePoint 项目

1. 定义具有表示要添加到 SharePoint 项目的属性的公共属性的类。 如果你想要添加多个属性，可以定义所有属性，在同一个类或不同的类中。

2. 在<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A>方法将<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>实现、 句柄<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested>的事件*projectService*参数。

3. 中的事件处理程序<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested>事件，将添加到你属性类的实例<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A>事件自变量参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何将两个属性添加到 SharePoint 项目。 一个属性保留其项目用户选项文件中的数据 ( *。 csproj.user*文件或 *。 vbproj.user*文件)。 其他属性保留其在项目文件中的数据 (*.csproj*文件或 *.vbproj*文件)。

 [!code-vb[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#1)]
 [!code-csharp[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#1)]

### <a name="understand-the-code"></a>理解代码
 若要确保在同一个实例`CustomProjectProperties`每次使用类<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested>事件发生时，代码示例将添加到的属性对象<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>的第一个项目时将发生此事件的属性。 再次发生此事件时，代码将检索此对象。 有关使用详细信息<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>属性以将数据与项目中，请参阅[关联自定义数据与 SharePoint 工具扩展](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 保存属性值，更改**设置**属性访问器使用以下 Api:

- `CustomUserFileProperty` 使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A>属性以将其值保存到项目用户选项文件。

- `CustomProjectFileProperty` 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A>方法以将其值保存到项目文件。

  有关这些文件中保存数据的详细信息，请参阅[将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以定义自定义属性的显示方式和行为**属性**通过应用中的属性窗口<xref:System.ComponentModel>到属性定义的命名空间。 以下属性可在许多情况下：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定将出现在属性的名称**属性**窗口。

- <xref:System.ComponentModel.DescriptionAttribute>：指定显示的说明字符串中的底部**属性**窗口时选择了该属性。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在显示的字符串之间的自定义转换**属性**窗口和一个非字符串属性值。

- <xref:System.ComponentModel.EditorAttribute>：指定要用于修改属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.Shell

- Microsoft.VisualStudio.Shell.Interop

- Microsoft.VisualStudio.Shell.Interop.8.0

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：将快捷菜单项添加到 SharePoint 项目](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
