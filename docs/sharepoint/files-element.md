---
title: Files 元素 |Microsoft Docs
description: 查看有关 Files 元素的参考信息，该元素是 SharePoint 项目项架构中的一个元素。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Files element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 03473f40bb78c866f3d93dea11a20b8747afad7b
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672803"
---
# <a name="files-element"></a>Files 元素
  指定要与 SharePoint 项目项一起部署的文件，例如功能元素文件和依赖非 SharePoint 项目的输出。

## <a name="syntax"></a>语法

```xml
<Files>
  <ProjectItemFile.../>
  <ProjectOutputFile.../>
</Files>
```

## <a name="type"></a>类型
 **FileCollectionType**

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|可选的 **ProjectItemFileType** 元素。<br /><br /> 表示在将项目项部署到 SharePoint 时要包含的 SharePoint 文件（如功能元素文件）。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|可选的 **ProjectOutputFileType** 元素。<br /><br /> 表示在将项目项部署到 SharePoint 时要包含的项目的输出。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素是文件必需的根元素 `.spdata` 。|

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
