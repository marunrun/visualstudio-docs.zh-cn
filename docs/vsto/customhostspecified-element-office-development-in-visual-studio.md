---
title: '&lt;p o i&gt;元素 （Visual Studio 中的 Office 开发）'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customHostSpecified> element
- <customHostSpecified> element
- customHostSpecified element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 26597796c99d3ab8740812819cf3aa5568e2985b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62956174"
---
# <a name="ltcustomhostspecifiedgt-element-office-development-in-visual-studio"></a>&lt;p o i&gt;元素 （Visual Studio 中的 Office 开发）
  `customHostSpecified`元素指示此解决方案不是独立的应用程序。 Office 解决方案包含承载于 Microsoft Office 应用程序内的组件。

## <a name="syntax"></a>语法

```xml
<customHostSpecified />
```

## <a name="elements-and-attributes"></a>元素和属性
 `customHostSpecified`元素是必需的 Office 解决方案。 此元素处于`co.v1`命名空间和指定此部署包含一个组件，将在自定义主机内部署并不是独立的应用程序。

 此元素是子元素的第一个`<entrypoint>`应用程序清单中的元素。 可以有其他子元素中的`<entrypoint>`元素或[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]在安装过程中，将引发验证错误。

 此元素不具有属性和任何子元素。

## <a name="example"></a>示例
 下面的代码示例说明了`customHostSpecified`Office 解决方案的应用程序清单中的元素。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

```xml
<entryPoint>
    <co.v1:customHostSpecified />
</entryPoint>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)