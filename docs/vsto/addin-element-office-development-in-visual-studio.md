---
title: '&lt;addin &gt; 元素（Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <addIn> element
- addin element
- <addin> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cf922799301aef67ee70c480dd9e0823382cbd47
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543762"
---
# <a name="ltaddingt-element-office-development-in-visual-studio"></a>&lt;addin &gt; 元素（Visual Studio 中的 Office 开发）
  命名空间的**addin**元素 `vstav3` 包含特定于在 Visual Studio 中开发的 Microsoft Office VSTO 外接程序和文档级自定义项的信息。

## <a name="syntax"></a>语法

```xml
<addIn>
  <entryPointsCollection>
    <entryPoints>
      <entryPoint>
      </entryPoint>
    </entryPoints>
  </entryPointsCollection>
  <update></update>
  <postActions>
    <postAction>
      <postActionData>
      </postActionData>
    <postAction>
  </postActions>
  <application>
    <customization>
    </customization>
  </application
</addIn>
```

## <a name="elements-and-attributes"></a>元素和属性
 命名空间的**addin**元素 `vstav3` 包含有关 Office 解决方案和 Microsoft Office 应用程序的信息。 此元素必须在以下命名空间中： `vstav3=urn:schemas-microsoft-com:vsta.v3`。 子元素也必须在此命名空间中。

 `addin` 元素没有属性。

 `addin` 元素具有以下子元素。

### <a name="entrypoints"></a>entryPoints
 必需。 [&#60;s&#62; 元素 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md)中介绍了**s**元素。

### <a name="update"></a>更新
 必需。 [&#40;Visual Studio 中的 Office 开发&#41;中&#60;更新&#62; 元素](../vsto/update-element-office-development-in-visual-studio.md)中介绍了**update**元素。

### <a name="postactions"></a>postActions
 可选。 [&#60;postActions&#62; 元素 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/postactions-element-office-development-in-visual-studio.md)中介绍了**postActions**元素。

### <a name="application"></a>application
 必需。 [&#40;Visual Studio 中的 Office 开发&#41;中&#60;应用程序&#62; 元素](../vsto/application-element-office-development-in-visual-studio.md)中描述了**应用程序**元素。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="description"></a>描述
 下面的代码示例说明了使用部署的文档级 Office 解决方案中的**addin**元素 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstav3:addIn
  xmlns:vstav3="urn:schemas-microsoft-com:vsta.v3">
  <vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.ThisWorkbook">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet1">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet2">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet3">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
  <vstav3:update
    enabled="true">
    <vstav3:expiration
      maximumAge="7"
      unit="days" />
  </vstav3:update>
  <vstav3:application>
    <vstov4:customizations
      xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
      <vstov4:customization>
        <vstov4:document
          solutionId="73e" />
      </vstov4:customization>
    </vstov4:customizations>
  </vstav3:application>
</vstav3:addIn>
```

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 下面的代码示例演示应用程序级 Office 解决方案中的**addin**元素，该解决方案是使用部署的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstav3:addIn
  xmlns:vstav3="urn:schemas-microsoft-com:vsta.v3">
  <vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoOutlookAddIn.ThisAddIn">
        <assemblyIdentity
          name="ContosoOutlookAddIn"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
  <vstav3:update
    enabled="true">
    <vstav3:expiration
      maximumAge="7"
      unit="days" />
  </vstav3:update>
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
</vstav3:addIn>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)