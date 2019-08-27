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
ms.openlocfilehash: 57c491c79030eea1a01024235c01aec425d5994c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62562357"
---
# <a name="projectitemfile-element"></a>ProjectItemFile 元素
  表示 SharePoint 文件，如功能元素文件部署到 SharePoint 时，包含与项目项。

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

|特性|描述|
|---------------|-----------------|
|**源**|所需**xs: string**属性。<br /><br /> 要使用的项目项部署的文件的名称。|
|**Target**|可选**xs: string**属性。<br /><br /> 该文件将在其中部署在 SharePoint，相对于部署根文件夹路径。 部署根文件夹由指定的部署类型**类型**属性。 如果**目标**属性未指定，则文件将被部署到一个文件夹中指定的名称与**源**属性。<br /><br /> 有关详细信息，请参阅的说明**部署路径**并**Deployment Root**属性的 SharePoint 项目项中的[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)。|
|**Type**|所需**xs: string**属性。<br /><br /> 部署文件的类型。 有关可能的值的详细信息，请参阅的说明**部署类型**属性中的 SharePoint 项目项[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[文件](../sharepoint/files-element.md)|指定要部署到 SharePoint 时，包含与 SharePoint 项目项的文件。|

## <a name="remarks"></a>备注
 通常在中引用的 SharePoint 文件**ProjectItemFile**元素包括功能元素文件 (*Elements.xml*)，为列表定义的架构文件 (*Schema.xml*)，和 Web 部件的 Web 部件定义文件 (*.webpart*)。

## <a name="element-information"></a>元素信息

|||
|-|-|
|**命名空间**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
