---
title: '&lt;description &gt; 元素 (ClickOnce 部署) |Microsoft Docs'
description: Description 元素标识用于在 "控制面板" 中创建 shell 存在和 "添加或删除程序" 项的应用程序信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#description
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <description> element [ClickOnce deployment manifest]
ms.assetid: 18f6919e-a3ab-4942-a57d-167fabfac44e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4eb1de8f5692eedc9673f1a22cb448ac8d102ae5
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2020
ms.locfileid: "94382827"
---
# <a name="ltdescriptiongt-element-clickonce-deployment"></a>&lt;description &gt; 元素 (ClickOnce 部署) 
标识用于在 "控制面板" 中创建 shell 存在和 " **添加或删除程序** " 项的应用程序信息。

## <a name="syntax"></a>语法

```xml

      <description 
   publisher 
   product
   suiteName
   supportUrl
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `description` 元素是必需的，它位于 `urn:schemas-microsoft-com:asm.v1` 命名空间中。 它不包含任何子元素，并且具有以下属性。

|属性|说明|
|---------------|-----------------|
|`publisher`|必需。 将部署配置为安装时，标识用于 Windows **开始** 菜单和 "控制面板" 中 " **添加或删除程序** " 项中的图标位置的公司名称。|
|`product`|必需。 标识完整的产品名称。 用作在 Windows " **开始** " 菜单中安装的图标的标题。|
|`suiteName`|可选。 标识 `publisher` Windows " **开始** " 菜单中的文件夹内的子文件夹。|
|`supportUrl`|可选。 指定在 "控制面板" 的 " **添加或删除程序** " 项中显示的支持 URL。 如果将部署配置为安装，则还会为 Windows " **开始** " 菜单中的应用程序支持创建此 URL 的快捷方式。|

## <a name="remarks"></a>注解
 Description 元素在所有部署配置中都是必需的。

## <a name="example"></a>示例
 下面的代码示例阐释了 `description` 部署清单中的元素 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 此代码示例是为 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md) 主题提供的更大示例的一部分。

```xml
<description
  asmv2:publisher="My Company Name"
  asmv2:product="My Application"
  xmlns="urn:schemas-microsoft-com:asm.v1" />
```

## <a name="see-also"></a>请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)