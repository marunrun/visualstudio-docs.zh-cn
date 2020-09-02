---
title: 创建 SharePoint 功能 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
- features [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8d3f453770dbb389a688db0a9edcc8e97e179858
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62952731"
---
# <a name="create-sharepoint-features"></a>创建 SharePoint 功能
  您可以使用 SharePoint 功能对相关 SharePoint 项目项进行分组，以便更轻松地进行部署。 使用 SharePoint 功能设计器，可以创建功能，设置作用域，并将其他功能标记为依赖项。 设计器还生成清单，清单是描述每个功能的 XML 文件。

## <a name="add-features-to-the-sharepoint-solution"></a>向 SharePoint 解决方案添加功能
 您可以使用解决方案资源管理器或 "打包资源管理器" 将功能添加到 SharePoint 解决方案。 您可以使用以下方法之一来添加功能。

- 在 **解决方案资源管理器**中，打开 " **功能**" 的快捷菜单，然后选择 " **添加功能**"。

- 在 " **打包资源管理器**" 中，打开包的快捷菜单，然后选择 " **添加功能**"。

## <a name="using-the-feature-designer"></a>使用功能设计器
 SharePoint 解决方案可以包含一个或多个 SharePoint 功能，这些功能分组到解决方案资源管理器中的功能节点下。 每个功能都有自己的 **功能设计器** ，可用于自定义功能属性。 有关详细信息，请参阅 [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)。 若要区分不同的功能，可以配置功能属性，例如标题、说明、版本和范围。

### <a name="feature-designer-options"></a>功能设计器选项
 创建功能后，可以使用功能设计器对其进行自定义。

 下表介绍了功能设计器中显示的功能属性。

|属性|说明|
|--------------|-----------------|
|Title|可选。 功能的默认标题设置为 "*解决方案名称* *FeatureName*" 功能名称。|
|说明|可选。 SharePoint 功能的说明。|
|范围|必需。 如果功能是使用 **解决方案资源管理器**创建的，则默认情况下，作用域设置为 Web。<br /><br /> -场：为整个服务器场激活一项功能。<br /><br /> -Site：为网站集中的所有网站激活某个功能。<br /><br /> -Web：激活特定网站的功能。<br /><br /> -WebApplication：为 web 应用程序中的所有网站激活某个功能。|
|解决方案中的项|可以添加到功能的所有 SharePoint 项。|
|功能中的项|已添加到功能中的 SharePoint 项目项。|

## <a name="add-and-remove-sharepoint-project-items"></a>添加和删除 SharePoint 项目项
 你可以选择要为部署添加 SharePoint 功能的 SharePoint 项目项。 使用 **功能设计器** 可以向功能中添加和移除项，并可以查看功能清单。 有关详细信息，请参阅 [如何：在 SharePoint 功能中添加和移除项](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)。

## <a name="add-feature-dependencies"></a>添加功能依赖项
 你可以配置功能清单，以便 SharePoint 服务器在激活功能之前激活某些功能。 例如，如果 SharePoint 功能依赖于功能或数据的其他功能，则 SharePoint 服务器可以首先尝试激活功能所依赖的任何功能。 有关详细信息，请参阅 [如何：添加和删除功能依赖项](../sharepoint/how-to-add-and-remove-feature-dependencies.md)。

## <a name="see-also"></a>另请参阅
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：在 SharePoint 功能中添加和移除项](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
- [如何：添加和移除功能依赖项](../sharepoint/how-to-add-and-remove-feature-dependencies.md)
