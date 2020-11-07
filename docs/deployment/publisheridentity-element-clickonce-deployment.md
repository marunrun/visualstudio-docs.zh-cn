---
title: '&lt;&gt; (ClickOnce 部署) 的 publisherIdentity 元素 |Microsoft Docs'
description: PublisherIdentity 元素包含有关为部署清单签名的发布服务器的信息。 签名清单需要元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publisherIdentity Element [ClickOnce deployment manifest], introduction
- required element for signed manifests [ClickOnce], publisherIdentity Element
- publisherIdentity Element [ClickOnce deployment manifest], syntax, elements, and attributes
ms.assetid: 34c579db-d2f2-4b66-b9c8-47207f33d950
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1eb4b67bfdca13c63480f3dde82004d87cd4a12a
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94350681"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;&gt; (ClickOnce 部署的 publisherIdentity 元素) 
包含有关为此部署清单签名的发布者的信息。

## <a name="syntax"></a>语法

```xml
<publisherIdentity
   name
   issuerKeyHash
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `publisherIdentity`签名清单需要元素。 下表显示 `publisherIdentity` 元素支持的属性。

|特性|说明|
|---------------|-----------------|
|`name`|必需。 描述发布此应用程序的参与方的标识。|
|`issuerKeyHash`|必需。 包含证书颁发者的公钥的 SHA-1 哈希。|

#### <a name="parameters"></a>参数

## <a name="property-valuereturn-value"></a>属性值/返回值

## <a name="exceptions"></a>例外

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求

## <a name="subhead"></a>副标题