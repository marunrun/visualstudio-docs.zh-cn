---
title: '&lt;v &gt; 元素（Visual Studio 中的 Office 开发）'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <vstoRuntime> element
- <vstoRuntime> element
- vstoRuntime element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 985afe50d7c6edcfdb34e2ca046f59c5f7b664a0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541877"
---
# <a name="ltvstoruntimegt-element-office-development-in-visual-studio"></a>&lt;v &gt; 元素（Visual Studio 中的 Office 开发）
  `vstoRuntime` 命名空间的 `vstav3` 元素包含针对特定 Office 解决方案的受支持的 Visual Studio Tools for Office Runtime 版本。

## <a name="syntax"></a>语法

```xml
<vstoRuntime
    release
    version
    supportUrl />
```

## <a name="elements-and-attributes"></a>元素和属性
 `vstoRuntime` 元素是必需的，它位于 `vstav3` 命名空间中。 如果 Office 解决方案支持两个版本的 Visual Studio Tools for Office Runtime，则应用程序清单中存在两个 `vstoRuntime` 元素。

 `vstoRuntime` 元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`release`|必需。 Visual Studio Tools for Office Runtime 的发布版本。|
|`version`|必需。 Visual Studio Tools for Office Runtime 的版本号。|
|`supportUrl`|可选。 指向 Visual Studio Tools for Office Runtime 安装位置的链接。|

 `vstoRuntime` 不包含任何元素。

## <a name="example"></a>示例
 下面的代码示例演示 Office 解决方案的应用程序清单中的 `vstoRuntime` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

```xml
<vstav3:vstoRuntime
    release="VSTOR40Beta1"
    version="10.0.20303"
    supportUrl="http://www.microsoft.com" />
```

## <a name="see-also"></a>另请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
