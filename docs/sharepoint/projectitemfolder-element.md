---
title: ProjectItemFolder 元素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFolder element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 38f8f70cc6480554441809e33c4083735600fbbb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539810"
---
# <a name="projectitemfolder-element"></a>ProjectItemFolder 元素
  表示映射文件夹。

## <a name="syntax"></a>语法

```xml
<ProjectItemFolder Target = "Path of SharePoint folder the mapped folder corresponds to"
    Type = "Type of deployment for the mapped folder" />
```

## <a name="type"></a>类型
 **ProjectItemFolderType**

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|**Target**|必需的**xs： string**特性。<br /><br /> SharePoint 安装中映射文件夹相对于部署根文件夹的对应文件夹的路径。 部署根文件夹由**type**特性指定的部署类型决定。<br /><br /> 有关详细信息，请参阅[开发 sharepoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中的 sharepoint 项目项的**部署路径**和**部署根**属性的说明。|
|类型|必需的**xs： string**特性。<br /><br /> 映射文件夹的部署类型。 有关可能值的详细信息，请参阅[开发 sharepoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中 sharepoint 项目项的**部署类型**属性的说明。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素是*spdata*文件必需的根元素。|

## <a name="remarks"></a>备注
 有关映射文件夹的详细信息，请参阅[如何：添加和删除映射文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

## <a name="element-information"></a>元素信息

|Property|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [如何：添加和移除映射文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)
