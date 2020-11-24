---
title: SafeControls 元素 |Microsoft Docs
description: 获取有关 SafeControls 元素的信息，该元素包含在 SharePoint 站点的 ASPX 页上标记为 "安全访问" 的 ASPX 控件或 web 部件的集合。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControls element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c3423d1b6efd106ef7f947bd8573dcd1aa548a66
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2020
ms.locfileid: "95440670"
---
# <a name="safecontrols-element"></a>SafeControls 元素
  ASPX 控件和 Web 部件的集合，指定为任何用户在 SharePoint 站点上的任何 ASPX 页上访问的安全。

## <a name="syntax"></a>语法

```xml
<SafeControls>
  <SafeControl.../>
</SafeControls>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[SafeControl](../sharepoint/safecontrol-element.md)|可选元素。<br /><br /> 表示一个 ASPX 控件或 Web 部件，在 SharePoint 站点上的任何 ASPX 页上，此控件或 Web 部件被指定为安全，可供任何用户访问。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素是 *spdata* 文件必需的根元素。|

## <a name="remarks"></a>注解
 有关安全控件的详细信息，请参阅 [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
