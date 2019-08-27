---
title: '&lt;entryPointsCollection&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <entryPointsCollection> element
- application manifests [Office development in Visual Studio], <entryPointsCollection> element
- entryPointsCollection element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4e877e186538622b3604e850040cbed0b018911d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951887"
---
# <a name="ltentrypointscollectiongt-element-office-development-in-visual-studio"></a>&lt;entryPointsCollection&gt;元素 （Visual Studio 中的 Office 开发）
  `entryPointsCollection` 命名空间的 `vstav3` 元素包含所有与 Office 解决方案关联的 `entryPoints` 元素。

## <a name="syntax"></a>语法

```xml
<entryPointsCollection>
  <entryPoints>
    <entryPoint>
    </entryPoint>
    <entryPoint>
    </entryPoint>
    <entryPoint>
    </entryPoint>
  </entryPoints>
</entryPointsCollection>
```

## <a name="elements-and-attributes"></a>元素和属性
 `entryPointsCollection` 元素是必需的，它位于 `vstav3` 命名空间中。 子元素也必须在此命名空间中。 在应用程序清单中定义的 `entryPointsCollection` 元素只有一个。

 `entryPointsCollection` 元素没有属性。

 `entryPointsCollection` 具有下列元素。

### <a name="entrypoints"></a>entryPoints
 必需。 角色`entryPoints`中的元素`vstav3`中定义命名空间[&#60;的入口点&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md)。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="description"></a>描述
 下面的代码示例演示使用 `entryPointsCollection` 部署的文档级解决方案的应用程序清单中的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]元素。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
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
```

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 下面的代码示例演示应用程序级解决方案的应用程序清单中的 `entryPointsCollection` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
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
```

## <a name="multi-project-deployment-example"></a>多项目部署示例

### <a name="description"></a>描述
 下面的代码示例演示使用两个 Office 解决方案进行的多项目部署的应用程序清单中的 `entryPointsCollection` 元素。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstav3:entryPointsCollection>
      <vstav3:entryPoints
        id="ContosoExcel">
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
      <vstav3:entryPoints
        id="ContosoOutlook">
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
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)