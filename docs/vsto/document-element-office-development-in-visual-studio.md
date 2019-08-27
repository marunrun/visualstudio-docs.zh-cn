---
title: '&lt;文档&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document element
- application manifests [Office development in Visual Studio], <document> element
- <document> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 36d822d60d1a28d48f660f6d358b75bf4a913048
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000023"
---
# <a name="ltdocumentgt-element-office-development-in-visual-studio"></a>&lt;文档&gt;元素 （Visual Studio 中的 Office 开发）
  `document`元素的`vstov4`命名空间存储文档级自定义的特定于自定义的信息。

## <a name="syntax"></a>语法

```xml
<document solutionId />
```

## <a name="elements-and-attributes"></a>元素和属性
 仅对于文档级自定义项必需。 `document` 元素位于 `vstov4` 命名空间中。 `document` 元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|`solutionId`|必需。 Visual Studio Tools for Office 运行时用于唯一标识的文档级解决方案的 GUID。 此值存储为 _AssemblyLocation 自定义文档属性。 有关详细信息，请参阅[自定义文档属性概述](../vsto/custom-document-properties-overview.md)。|

 `document` 无子元素。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="description"></a>描述
 下面的代码示例演示`document`通过使用部署的文档级 Office 解决方案中的元素[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:document
  solutionId="73e" />
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)