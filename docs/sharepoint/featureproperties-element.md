---
title: FeatureProperties 元素 |Microsoft Docs
description: 查看有关 FeatureProperties 元素的参考信息，该元素是 SharePoint 项目项架构中的一个元素。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperties element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9ee2bddec02263a889fb1f69088a8a50b3d8b57d
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672595"
---
# <a name="featureproperties-element"></a>FeatureProperties 元素
  在将功能部署到 SharePoint 时包含的属性值的集合。 部署功能后，可以在代码中访问属性值。

## <a name="syntax"></a>语法

```xml
<FeatureProperties>
  <FeatureProperty.../>
</FeatureProperties>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[FeatureProperty](../sharepoint/featureproperty-element.md)|可选元素。<br /><br /> 表示键/值格式的自定义属性。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素是文件必需的根元素 `.spdata` 。|

## <a name="remarks"></a>注解
 有关功能属性的详细信息，请参阅 [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。

## <a name="element-information"></a>元素信息

|元素|说明|
|-------------|-----------------|
|**命名空间**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
