---
title: 将数据保存在 SharePoint 项目系统的扩展 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- SharePoint project items, saving string data
- project items [SharePoint development in Visual Studio], saving string data
- projects [SharePoint development in Visual Studio], saving string data
- SharePoint projects, saving string data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 52b04490a646c7ced27d4a2d7f2344e27cbbae8b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827240"
---
# <a name="save-data-in-extensions-of-the-sharepoint-project-system"></a>将数据保存在 SharePoint 项目系统的扩展
  扩展 SharePoint 项目系统时，可以保存字符串数据的 SharePoint 项目关闭后仍然存在。 数据是与特定项目项或项目本身通常相关联。

 如果有不需要保留的数据，可以将数据添加到实现 SharePoint 工具对象模型中的任何对象<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject>接口。 有关详细信息，请参阅[关联自定义数据与 SharePoint 工具扩展](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

## <a name="save-data-that-is-associated-with-a-project-item"></a>保存与项目项关联的数据
 如果具有与特定的 SharePoint 项目项，如您将添加到项目项属性的值相关联的数据可以保存到数据 *.spdata*项目项文件。 若要执行此操作，请使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>属性的<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>对象。 添加到此属性的数据保存在**ExtensionData**中的元素 *.spdata*项目项文件。 有关详细信息，请参阅[ExtensionData 元素](../sharepoint/extensiondata-element.md)。

 下面的代码示例演示如何使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>属性将保存在自定义的 SharePoint 项目项类型中定义的字符串属性的值。 若要查看此上下文中的一个更大示例的示例，请参阅[如何：将属性添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#14](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#14)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#14](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#14)]

## <a name="save-data-that-is-associated-with-a-project"></a>保存与项目相关联的数据
 如果具有项目级别的数据，例如 SharePoint 项目中添加的属性的值可以将数据保存到项目文件 ( *.csproj*文件或 *.vbproj*文件) 或项目用户选项文件 ( *。 csproj.user*文件或 *。 vbproj.user*文件)。 想要使用的数据的方式取决于您选择将保存在数据文件：

- 如果你想要的所有开发人员可以打开 SharePoint 项目的数据，将数据保存到项目文件。 此文件是始终签入到源代码管理数据库，因此此文件中的数据的其他开发人员可以签出该项目。

- 如果你想要仅对当前具有开发人员在 Visual Studio 中打开 SharePoint 项目可用的数据，将数据保存到项目用户选项文件。 此文件是不通常签入到源代码管理数据库，因此此文件中的数据不可用的其他开发人员签出该项目。

### <a name="save-data-to-the-project-file"></a>将数据保存到项目文件
 若要将数据保存到项目文件，将转换<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>对象传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>对象，以及如何将<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A>方法。 下面的代码示例演示如何使用此方法将保存到项目文件的项目属性的值。 若要查看此示例中的上下文中更大的示例，请参阅[如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

 [!code-vb[SpExt_SPCustomPrjProperty#3](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#3)]
 [!code-csharp[SpExt_SPCustomPrjProperty#3](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#3)]

 有关转换的详细信息<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>对象与其他类型中的 Visual Studio 自动化对象模型或集成对象模型，请参阅[SharePoint 项目系统类型与其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md).

### <a name="save-data-to-the-project-user-option-file"></a>将数据保存到项目用户选项文件
 若要将数据保存到项目用户选项文件，请使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A>属性的<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>对象。 下面的代码示例演示如何使用此属性将保存到项目用户选项文件的项目属性的值。 若要查看此示例中的上下文中更大的示例，请参阅[如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

 [!code-vb[SpExt_SPCustomPrjProperty#2](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#2)]
 [!code-csharp[SpExt_SPCustomPrjProperty#2](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#2)]

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [SharePoint 项目系统类型与其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
