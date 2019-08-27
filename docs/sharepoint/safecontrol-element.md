---
title: SafeControl 元素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControl element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e6b47254a80c9cdadab6ca18f2fb8c3e8540fbd0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827332"
---
# <a name="safecontrol-element"></a>SafeControl 元素
  表示一个 ASPX 控件或指定为安全的任何用户访问 SharePoint 站点上任何 ASPX 页上的 Web 部件。

## <a name="syntax"></a>语法

```xml
<SafeControl Assembly = "Name of assembly that contains the safe control"
    IsSafe = "true/false"
    IsSafeAgainstScript = "true/false"
    Name = "Name of this safe control entry"
    Namespace = "Namespace of the safe control"
    TypeName = "Type of the safe control" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|**Assembly**|可选**xs: string**属性。<br /><br /> 定义 Web 部件的 ASPX 控件的程序集的名称。 默认情况下，此特性使用 **$SharePoint.Project.AssemblyFullName$** 可替换参数的程序集名称。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。|
|**IsSafe**|可选**xs: boolean**属性。<br /><br /> 指定 Web 部件的 ASPX 控件是不受信任的用户可以访问安全。|
|**IsSafeAgainstScript**|可选**xs: boolean**属性。<br /><br /> 指定不受信任的用户是否可以查看或编辑 Web 部件的 ASPX 控件的属性。|
|**名称**|可选**xs: string**属性。<br /><br /> 此集合中的安全控件项的名称。|
|**命名空间**|可选**xs: string**属性。<br /><br /> Web 部件的 ASPX 控件的命名空间。|
|**TypeName**|可选**xs: string**属性。<br /><br /> Web 部件的 ASPX 控件的类型名称。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[SafeControls](../sharepoint/safecontrols-element.md)|表示的 ASPX 控件和指定为安全的任何用户访问 SharePoint 站点上任何 ASPX 页上的 Web 部件的集合。|

## <a name="remarks"></a>备注
 有关安全控件的详细信息，请参阅[提供在项目项中的打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。

## <a name="element-information"></a>元素信息

|||
|-|-|
|**命名空间**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [提供在项目项中的打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
