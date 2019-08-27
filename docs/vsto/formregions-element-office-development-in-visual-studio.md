---
title: '&lt;formRegions&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formRegions element
- <formRegions> element
- application manifests [Office development in Visual Studio], <formRegions> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 68a24560df1da153702cfca2a206ea38cc8fac94
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62972325"
---
# <a name="ltformregionsgt-element-office-development-in-visual-studio"></a>&lt;formRegions&gt;元素 （Visual Studio 中的 Office 开发）
  `formRegions`元素的`vstov4`命名空间包含与 VSTO 外接程序相关联的 Microsoft Office Outlook 窗体区域。

## <a name="syntax"></a>语法

```xml
<formRegions>
  <formRegion>
  </formRegion>
</formRegions>
```

## <a name="elements-and-attributes"></a>元素和属性
 `formRegions` 命名空间的 `vstov4` 元素包含 Outlook VSTO 外接程序的所有 `formRegion` 元素。 只有包括窗体区域的 Outlook VSTO 外接程序才需要该元素。

 在应用程序清单中定义的 `formRegions` 元素可能只有一个。

 `formRegions` 元素没有属性。

 `formRegions` 元素具有以下元素。

### <a name="formregion"></a>formRegion
 为包含窗体区域的 Outlook VSTO 外接程序所需。 `formRegion`中定义元素[ &#60;formRegion&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/formregion-element-office-development-in-visual-studio.md)。

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 下面的代码示例演示应用程序级 Office 解决方案的应用程序清单中的 `formRegions` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:formRegions>
  <vstov4:formRegion
      name="OutlookAddIn1.FormRegion1">
    <vstov4:messageClass name="IPM.Note" />
    <vstov4:messageClass name="IPM.Contact" />
    <vstov4:messageClass name="IPM.Appointment" />
  </vstov4:formRegion>
</vstov4:formRegions>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)