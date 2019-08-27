---
title: '&lt;应用程序&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <application> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 80652f6752b87cf0413b0b3166b0cf3292231c25
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62942892"
---
# <a name="ltapplicationgt-element-office-development-in-visual-studio"></a>&lt;应用程序&gt;元素 （Visual Studio 中的 Office 开发）
  `application` 命名空间的 `vstav3` 元素包装 Office 解决方案的描述。 对于文档级自定义项和 VSTO 外接程序，子元素是不同的。

## <a name="syntax-for-document-level-customizations"></a>对于文档级自定义项的语法

```xml
<application>
  <customization
    id
    <document
      solutionId
    />
  </customization>
</application>
```

## <a name="syntax-for-application-level-add-ins"></a>应用程序级加载项的语法

```xml
<application>
  <customization
    id
    <appAddin
      application
      loadBehavior
      keyName>
    <friendlyName></friendlyName>
    <description></description>
    <formRegions></formRegions>
  </customization>
</application>
```

## <a name="elements-and-attributes"></a>元素和属性
 `application` 命名空间的 `vstav3` 元素是包装 `vstov4` 命名空间中包含的所有自定义项特定信息的节点。

 `application` 元素没有属性。

 `application` 元素具有以下元素。

### <a name="customization"></a>自定义
 角色`customization`中的元素`vstov3`中定义命名空间[&#60;自定义&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/customization-element-office-development-in-visual-studio.md)。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="description"></a>描述
 下面的代码示例演示使用 `application` 部署的文档级 Office 解决方案中的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]元素。 此代码示例摘自 [Application Manifests for Office Solutions](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大的示例。

### <a name="code"></a>代码

```xml
<vstav3:application>
  <vstov4:customizations
    xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
    <vstov4:customization>
      <vstov4:document
        solutionId="73e" />
    </vstov4:customization>
  </vstov4:customizations>
</vstav3:application>
```

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 以下代码示例演示使用 `application` 部署的应用程序级 Office 解决方案中的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]元素。 此代码示例摘自 [Application Manifests for Office Solutions](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大的示例。

### <a name="code"></a>代码

```xml
<vstav3:application>
  <vstov4:customizations
    xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
    <vstov4:customization>
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
    </vstov4:customization>
  </vstov4:customizations>
</vstav3:application>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)