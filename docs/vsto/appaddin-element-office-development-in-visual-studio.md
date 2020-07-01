---
title: '&lt;appAddin &gt; 元素（Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
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
ms.openlocfilehash: 1bf9ea990d12bd24adee3f6a24a39fa43c74fb71
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531633"
---
# <a name="ltappaddingt-element-office-development-in-visual-studio"></a>&lt;appAddin &gt; 元素（Visual Studio 中的 Office 开发）
  命名空间的**appAddin**元素 `vstov4` 存储 VSTO 外接程序特定于自定义项的信息。

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
 **AppAddin**元素是必需的，它位于 `vstov4` 命名空间中。 在应用程序清单中只定义了一个**appAddin**元素。

 **AppAddin**元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|**应用程序**|必需。 标识 Microsoft Office 应用程序。 值可以是以下值之一：Excel、InfoPath、Outlook、PowerPoint、Project、Visio 或 Word。|
|**loadBehavior**|可选。 默认情况下，通过将此值设置为来启用**loadBehavior** 。 为进行调试，可以通过将此值设置为 2 来禁用 VSTO 外接程序。 有关详细信息，请参阅[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)中标题为 LoadBehavior 的表。|
|**keyName**|必需。 此值是该应用程序将用于加载 VSTO 外接程序的注册表项名称。 有关详细信息，请参阅[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。|

 **AppAddin**元素具有以下子元素。

### <a name="friendlyname"></a>friendlyName
 可选。 [&#60;friendlyname&#62; 元素 &#40;Visual Studio 中的 Office 开发&#41;中](../vsto/friendlyname-element-office-development-in-visual-studio.md)介绍了**friendlyname**元素。

### <a name="description"></a>description
 可选。 **Description**元素在[Visual Studio&#41;中 &#40;Office 开发&#62; 元素&#60;说明](../vsto/description-element-office-development-in-visual-studio.md)中进行了说明。

### <a name="formregions"></a>formRegions
 仅为包含窗体区域的 Outlook VSTO 外接程序所需。 [&#60;s&#62; 元素 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/formregions-element-office-development-in-visual-studio.md)中介绍了**s**元素。

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 下面的代码示例说明了使用部署的 Outlook 解决方案中的**appAddin**元素 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

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