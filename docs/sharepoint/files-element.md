---
title: Files 元素 |Microsoft Docs
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
ms.openlocfilehash: 42e919bbe25047da14940203ac86793430aeadde
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546505"
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
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|可选的**ProjectItemFileType**元素。<br /><br /> 表示在将项目项部署到 SharePoint 时要包含的 SharePoint 文件（如功能元素文件）。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|可选的**ProjectOutputFileType**元素。<br /><br /> 表示在将项目项部署到 SharePoint 时要包含的项目的输出。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素是文件必需的根元素 `.spdata` 。|

## <a name="element-information"></a>元素信息

|properties|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
