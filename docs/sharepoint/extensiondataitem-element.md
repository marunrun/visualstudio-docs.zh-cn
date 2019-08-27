---
title: ExtensionDataItem 元素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionDataItem element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 658fb63227f4c4532038d537bde7cc10ca2c4f5e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967378"
---
# <a name="extensiondataitem-element"></a>ExtensionDataItem 元素
  自定义数据项中键/值格式的 SharePoint 项目项与相关联。 键和值必须为字符串。

## <a name="syntax"></a>语法

```xml
<ExtensionDataItem Key = "Key of the data item"
    Value = "Value of the data item" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|**Key**|所需**xs： 字符串**属性。<br /><br /> 用于存储和检索数据的项的键。|
|**值**|所需**xs: string**属性。<br /><br /> 数据项的值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|表示 SharePoint 项目项与相关联的自定义数据项的集合。|

## <a name="remarks"></a>备注
 在将自定义数据与 SharePoint 项目项使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A>的属性<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>对象时，Visual Studio 将数据保存到一个新**ExtensionDataItem**中的元素`.spdata`文件项目项。 有关详细信息，请参阅[将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

## <a name="element-information"></a>元素信息

|||
|-|-|
|**命名空间**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
