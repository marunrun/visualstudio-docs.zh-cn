---
title: ProjectOutputFile 元素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectOutputFile element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 12f399b7a09c18c77482475575ca387a11955762
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542384"
---
# <a name="projectoutputfile-element"></a>ProjectOutputFile 元素
  表示在将项目项部署到 SharePoint 时要包含的单独项目的输出。

## <a name="syntax"></a>语法

```xml
<ProjectOutputFile ProjectId = "GUID of the project"
    ProjectPath = "Relative path of the project"
    Target = "Deployment path of the project output"
    Type = "Type of deployment for the project output" />
```

## <a name="type"></a>类型
 **ProjectOutputFileType**

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**ProjectId**|必需的**xs： string**特性。<br /><br /> 要包括其输出的依赖项目的 GUID。 这对应于依赖项目文件中的**ProjectGuid**元素。|
|**ProjectPath**|必需的**xs： string**特性。<br /><br /> 包含要包含的输出的依赖项目的相对路径，包括项目文件名。 此路径相对于包含 SharePoint 项目项的 SharePoint 项目的根文件夹。|
|**Target**|可选**xs： string**特性。<br /><br /> 要在 SharePoint 服务器上部署依赖项目输出的路径（相对于部署根文件夹）。 部署根文件夹由**type**特性指定的部署类型决定。<br /><br /> 有关详细信息，请参阅[开发 sharepoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中的 sharepoint 项目项的**部署路径**和**部署根**属性的说明。|
|类型|必需的**xs： string**特性。<br /><br /> 用于依赖项目的输出的部署类型。 有关可能值的详细信息，请参阅[开发 sharepoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中 sharepoint 项目项的**部署类型**属性的说明。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[附件](../sharepoint/files-element.md)|指定将 SharePoint 项目项部署到 SharePoint 时要包含的文件。|

## <a name="remarks"></a>备注
 使用**ProjectOutputFile**元素将项目的输出包含在 SharePoint 项目项的部署中。 可以指定不同的项目，也可以指定包含项目项的项目。 有关详细信息，请参阅[在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。

## <a name="element-information"></a>元素信息

|properties|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
