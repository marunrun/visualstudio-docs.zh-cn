---
title: '&lt;&gt; (Visual Studio 中的 Office 开发更新元素) '
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- update element
- <update> element
- application manifests [Office development in Visual Studio], <update> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 241bddb8c79a01bb1ba6921486a4dc46d99940cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537379"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;&gt; (Visual Studio 中的 Office 开发更新元素) 
  `update`元素指定解决方案检查更新的时间间隔。

## <a name="syntax"></a>语法

```xml
<update
  enabled>
  <expiration
    maximumAge
    unit
  />
</update>
```

## <a name="elements-and-attributes"></a>元素和属性
 `update` 元素是必需的，它位于 `vstav3` 命名空间中。

 `update` 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`enabled`|必需。 将 "启用" 设置为以下值之一：<br /><br /> -   若要检查更新，**则为 true** 。<br />-   若要防止检查更新，**则为 false** 。|

 `update` 元素具有以下子元素。

### <a name="expiration"></a>expiration
 `expiration` 元素是必需的，它位于 `vstav3` 命名空间中。 此元素指定解决方案检查更新的时间间隔。

 `expiration` 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`maximumAge`| 必需。 将此设置为等于整数。|
|`unit`|必需。 设置 `unit` 为以下值之一：<br /><br /> -   **小时**<br />-   **天数**<br />-   **周**|

## <a name="example-of-always-checking-for-updates"></a>始终检查更新的示例

### <a name="description"></a>说明
 下面的代码示例演示了一个 `update` 元素，该元素设置为在 Office 解决方案中始终检查更新。

### <a name="code"></a>代码

```xml
<vstav3:update enabled="true" />
```

## <a name="example-of-setting-a-default-update-interval"></a>设置默认更新间隔的示例

### <a name="description"></a>说明
 下面的代码示例演示 `update` Office 解决方案的应用程序清单中的元素。 此代码示例是 [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstav3:update enabled="true">
    <vstav3:expiration maximumAge="7" unit="days" />
</vstav3:update>
```

## <a name="see-also"></a>请参阅

- [使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
