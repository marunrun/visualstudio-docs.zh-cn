---
title: '&lt;appAddin&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <appAddin> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2116576acb06e6291749d9c0176fcf4ebb426739
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62953239"
---
# <a name="ltappaddingt-element-office-development-in-visual-studio"></a>&lt;appAddin&gt;元素 （Visual Studio 中的 Office 开发）
  **AppAddin**元素的`vstov4`命名空间存储 VSTO 外接程序的特定于自定义的信息。

## <a name="syntax"></a>语法

```xml
<appAddin
  application
  loadBehavior
  keyName>
  <friendlyName>
  <description>
  <formRegions></formRegions>
</appAddin>
```

## <a name="elements-and-attributes"></a>元素和属性
 **AppAddin**元素是必需的它位于`vstov4`命名空间。 只有一个**appAddin**应用程序清单中定义的元素。

 **AppAddin**元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|**application**|必需。 标识 Microsoft Office 应用程序。 值可以是下列任一值：Excel、 InfoPath、 Outlook、 PowerPoint、 项目、 Visio 或 Word。|
|**loadBehavior**|可选。 默认情况下**loadBehavior**情况下此值设置为启用。 为进行调试，可以通过将此值设置为 2 来禁用 VSTO 外接程序。 有关详细信息，请参阅标题为 LoadBehavior 值中的表[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。|
|**keyName**|必需。 此值是该应用程序将用于加载 VSTO 外接程序的注册表项名称。 有关详细信息，请参阅[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。|

 **AppAddin**元素具有下列子元素。

### <a name="friendlyname"></a>FriendlyName
 可选。 **FriendlyName**元素所述[ &#60;friendlyName&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/friendlyname-element-office-development-in-visual-studio.md)。

### <a name="description"></a>说明
 可选。 **描述**元素所述[&#60;说明&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/description-element-office-development-in-visual-studio.md)。

### <a name="formregions"></a>formRegions
 仅为包含窗体区域的 Outlook VSTO 外接程序所需。 **FormRegions**元素所述[ &#60;formRegions&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/formregions-element-office-development-in-visual-studio.md)。

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 下面的代码示例演示**appAddin**部署使用的 Outlook 解决方案中的元素[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:appAddIn
  application="Outlook"
  loadBehavior="3"
  keyName="ContosoOutlookAddIn">
  <vstov4:friendlyName>
    ContosoOutlookAddIn
  </vstov4:friendlyName>
  <vstov4:description>
    ContosoOutlookAddIn - Outlook VSTO Add-in
    created with Visual Studio Tools for Office
  </vstov4:description>
  <vstov4:formRegions>
    <vstov4:formRegion
        name="OutlookAddIn1.FormRegion1">
      <vstov4:messageClass name="IPM.Note" />
      <vstov4:messageClass name="IPM.Contact" />
      <vstov4:messageClass name="IPM.Appointment" />
    </vstov4:formRegion>
  </vstov4:formRegions>
</vstov4:appAddIn>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)