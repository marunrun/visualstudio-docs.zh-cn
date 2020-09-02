---
title: SharePoint 项目项架构参考 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
- SafeControls element
- SafeControl element
- .spdata files
- ExtensionData element
- FeatureProperties element
- ProjectOutputFile element
- Files element
- ProjectItemFolder element
- ProjectItemFile element
- ExtensionDataItem element
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bc15ff5c384ec63f99ed50a5f3c700efd7ba3c18
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "63007714"
---
# <a name="sharepoint-project-item-schema-reference"></a>SharePoint 项目项架构参考
  Visual Studio 使用 SharePoint 项目项架构来验证 *spdata* 文件的内容。 *Spdata*文件指定 SharePoint 项目项的内容和行为。 有关 SharePoint 项目项的内容的详细信息，请参阅 [为 sharepoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 SharePoint 项目项架构名为 ProjectItemModelSchema，默认情况下安装在 (x86) % \ Microsoft Visual Studio 11.0 \ Xml\schemas 的% Program Files 中。

 根元素是 [项目](../sharepoint/projectitem-element.md) 项元素。 下表描述了该架构定义的所有元素。

|元素|说明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|表示与 SharePoint 项目项关联的自定义数据项的集合。|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|表示与 SharePoint 项目项关联的自定义数据项，以键/值格式表示。 键和值都必须是字符串。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|表示在将功能部署到 SharePoint 时包含的属性值的集合。 部署功能后，可以在代码中访问属性值。|
|[FeatureProperty](../sharepoint/featureproperty-element.md)|表示在将功能部署到 SharePoint 时包含的自定义属性。 部署功能后，可在代码中访问属性。|
|[文件](../sharepoint/files-element.md)|指定要与 SharePoint 项目项一起部署的文件，例如功能元素文件或项目的输出。|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|表示在将项目项部署到 SharePoint 时要包含的 SharePoint 文件（如功能元素文件）。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|表示映射文件夹。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|表示在将项目项部署到 SharePoint 时要包含的项目的输出。|
|[SafeControl](../sharepoint/safecontrol-element.md)|表示一个 ASPX 控件或 Web 部件，在 SharePoint 站点上的任何 ASPX 页上，此控件或 Web 部件被指定为安全，可供任何用户访问。|
|[SafeControls](../sharepoint/safecontrols-element.md)|表示 ASPX 控件和 Web 部件的集合，这些控件和在 SharePoint 站点上的任何 ASPX 页上被指定为可供任何用户访问的安全。|

## <a name="see-also"></a>另请参阅
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
