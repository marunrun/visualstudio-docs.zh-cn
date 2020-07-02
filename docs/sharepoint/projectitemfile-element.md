---
title: ProjectItemFile 元素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFile element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d1c9814498d74a5d1a6533576f1071b4bf7deb57
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539849"
---
# <a name="projectitemfile-element"></a>ProjectItemFile 元素
  表示在将项目项部署到 SharePoint 时要包含的 SharePoint 文件（如功能元素文件）。

## <a name="syntax"></a>语法

```xml
<ProjectItemFile Source = "Name of the file"
    Target = "Deployment path of the file"
    Type = "Type of deployment for the file" />
```

## <a name="type"></a>类型
 **ProjectItemFileType**

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|**Source**|必需的**xs： string**特性。<br /><br /> 要与项目项一起部署的文件的名称。|
|**Target**|可选**xs： string**特性。<br /><br /> 相对于部署根文件夹，将在 SharePoint 上部署文件的路径。 部署根文件夹由**type**特性指定的部署类型决定。 如果未指定**目标**属性，则会将该文件部署到**源**属性中指定的名称的文件夹中。<br /><br /> 有关详细信息，请参阅[开发 sharepoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中的 sharepoint 项目项的**部署路径**和**部署根**属性的说明。|
|类型|必需的**xs： string**特性。<br /><br /> 文件的部署类型。 有关可能值的详细信息，请参阅[开发 sharepoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中 sharepoint 项目项的**部署类型**属性的说明。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[附件](../sharepoint/files-element.md)|指定将 SharePoint 项目项部署到 SharePoint 时要包含的文件。|

## <a name="remarks"></a>备注
 通常在**ProjectItemFile**元素中引用的 SharePoint 文件包括功能元素文件（*Elements.xml*）、列表定义的架构文件（*Schema.xml*）以及 Web 部件（*webpart*）的 Web 部件定义文件。

## <a name="element-information"></a>元素信息

|Property|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
