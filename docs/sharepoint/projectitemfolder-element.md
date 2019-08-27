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
ms.openlocfilehash: 124716f8c40a8adc0a0ae1a28cda21dcb5e00ddf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62562697"
---
# <a name="projectitemfolder-element"></a>ProjectItemFolder 元素
  表示映射的文件夹。

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

|特性|描述|
|---------------|-----------------|
|**Target**|所需**xs： 字符串**属性。<br /><br /> 在 SharePoint 安装中映射的文件夹对应，相对于部署根文件夹的文件夹的路径。 部署根文件夹由指定的部署类型**类型**属性。<br /><br /> 有关详细信息，请参阅的说明**部署路径**并**Deployment Root**属性的 SharePoint 项目项中的[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)。|
|**Type**|所需**xs: string**属性。<br /><br /> 为映射文件夹部署的类型。 有关可能的值的详细信息，请参阅的说明**部署类型**属性中的 SharePoint 项目项[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素是必需的根元素 *.spdata*文件。|

## <a name="remarks"></a>备注
 有关映射的文件夹的详细信息，请参阅[如何： 添加和移除映射的文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

## <a name="element-information"></a>元素信息

|||
|-|-|
|**命名空间**|http:\/\/schemas.microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [如何： 添加和移除映射的文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)
