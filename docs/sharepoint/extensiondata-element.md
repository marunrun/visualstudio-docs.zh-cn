---
title: ExtensionData 元素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionData element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 192b745580ab676dab476b4dcf31c15b9095be2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967339"
---
# <a name="extensiondata-element"></a>ExtensionData 元素
  表示 SharePoint 项目项与相关联的自定义数据项的集合。

## <a name="syntax"></a>语法

```xml
<ExtensionData>
  <ExtensionDataItem.../>
</ExtensionData>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|可选元素。<br /><br /> 表示键/值格式中的 SharePoint 项目项与相关联的自定义数据项。 键和值必须为字符串。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素的必需的根元素的`.spdata`文件。|

## <a name="remarks"></a>备注
 在将自定义数据与 SharePoint 项目项使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>的属性<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>对象时，Visual Studio 将保存到数据**ExtensionData**中的元素`.spdata`项目文件项。 有关详细信息，请参阅[将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

## <a name="element-information"></a>元素信息

|||
|-|-|
|**命名空间**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
