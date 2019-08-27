---
title: '&lt;入口点&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <entryPoint> element
- <entryPoint> element
- entryPoint element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bd3da83a25a05690e56d229f61ee709473171dd7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62799779"
---
# <a name="ltentrypointgt-element-office-development-in-visual-studio"></a>&lt;入口点&gt;元素 （Visual Studio 中的 Office 开发）
  `entryPoint` 命名空间中的每个 `vstav3` 元素都标识应在安装此 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 应用程序时运行的自定义程序集。

## <a name="syntax"></a>语法

```xml
<entryPoint class>
    <assemblyIdentity />
</entryPoint>
```

## <a name="elements-and-attributes"></a>元素和属性
 `entryPoint` 元素是必需的，它位于 `vstav3` 命名空间中。

 每个 `entryPoint` 元素都只能包含一个自定义程序集。 应用程序清单中可以定义多个 `entryPoint` 元素。

 `entryPoint` 元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|`class`|必需。 标识要执行的自定义程序集。 此属性的语法是 *NamespaceName.ClassName*。|

 `entryPoint` 具有以下元素。

### <a name="assemblyidentity"></a>assemblyIdentity
 必需。 `assemblyIdentity` 命名空间中的 `vstav3` 元素引用 `assemblyIdentity` 应用程序清单中的现有 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 元素。

 角色`assemblyIdentity`，其属性的定义[ &#60;assemblyIdentity&#62;元素&#40;ClickOnce 应用程序&#41;](../deployment/assemblyidentity-element-clickonce-application.md)。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="description"></a>描述
 下面的代码示例演示文档级 Office 解决方案的应用程序清单中的 `entryPoint` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
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
```

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 下面的代码示例演示应用程序级 Office 解决方案的应用程序清单中的 `entryPoint` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstav3:entryPoint
  class="ContosoOutlookAddIn.ThisAddIn">
  <assemblyIdentity
    name="ContosoOutlookAddIn"
    version="1.0.0.0"
    language="neutral"
    processorArchitecture="msil" />
</vstav3:entryPoint>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)