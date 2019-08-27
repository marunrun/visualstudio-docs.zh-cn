---
title: '&lt;更新&gt;元素 （Visual Studio 中的 Office 开发）'
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 461fae79e3af346d64017166b6dae3ace67599e1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967528"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;更新&gt;元素 （Visual Studio 中的 Office 开发）
  `update`元素指定的更新的解决方案将检查的间隔。

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

|特性|描述|
|---------------|-----------------|
|`enabled`|必需。 将 enabled 设置为以下值之一：<br /><br /> -   **true**检查更新。<br />-   **false**以免检查更新。|

 `update` 元素具有以下子元素。

### <a name="expiration"></a>过期
 `expiration` 元素是必需的，它位于 `vstav3` 命名空间中。 此元素指定的解决方案检查更新的间隔。

 `expiration` 元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|`maximumAge`| 必需。 这将设置为一个整数。|
|`unit`|必需。 设置`unit`为以下值之一：<br /><br /> -   **小时数**<br />-   **days**<br />-   **周**|

## <a name="example-of-always-checking-for-updates"></a>始终检查更新的示例

### <a name="description"></a>描述
 下面的代码示例说明了`update`设置始终检查更新 Office 解决方案中的元素。

### <a name="code"></a>代码

```xml
<vstav3:update enabled="true" />
```

## <a name="example-of-setting-a-default-update-interval"></a>设置默认的更新时间间隔的示例

### <a name="description"></a>描述
 下面的代码示例说明了`update`Office 解决方案的应用程序清单中的元素。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

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
