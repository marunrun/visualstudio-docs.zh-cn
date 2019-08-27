---
title: '&lt;formRegion&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <formRegion> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 33bc2ce58f90f37a1219427558a01bd13e5654df
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62414528"
---
# <a name="ltformregiongt-element-office-development-in-visual-studio"></a>&lt;formRegion&gt;元素 （Visual Studio 中的 Office 开发）
  `formRegion`元素的`vstov4`命名空间标识与 VSTO 外接程序相关联的 Microsoft Office Outlook 窗体区域。

## <a name="syntax"></a>语法

```xml
<formRegion
  name>
  <messageClass
    name/>
</formRegion>
```

## <a name="elements-and-attributes"></a>元素和属性
 `formRegion` 命名空间的 `vstov4` 元素标识与 Outlook VSTO 外接程序关联的窗体区域。 只有包括窗体区域的 Outlook VSTO 外接程序才需要该元素。

 单个 VSTO 外接程序的一个 `formRegion` 元素中可以定义多个 `formRegions` 元素。

 `formRegion` 元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|`name`|必需。 标识窗体区域名称。|

 `formRegion` 元素具有以下子元素。

### <a name="messageclass"></a>messageClass
 `messageClass` 元素标识与窗体区域关联的 Outlook 窗体。

 `messageClass` 元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|`name`|必需。 标识与窗体区域关联的窗体。|

## <a name="example"></a>示例
 下面的代码示例阐释 Outlook VSTO 外接程序的应用程序清单中的 `formRegion` 元素，该外接程序是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 其中有三个邮件类与这一个窗体区域关联。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

```xml
<vstov4:formRegion
    name="OutlookAddIn1.FormRegion1">
  <vstov4:messageClass name="IPM.Note" />
  <vstov4:messageClass name="IPM.Contact" />
  <vstov4:messageClass name="IPM.Appointment" />
</vstov4:formRegion>
```

## <a name="see-also"></a>请参阅

- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)