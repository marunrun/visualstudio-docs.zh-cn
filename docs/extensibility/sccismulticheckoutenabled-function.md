---
title: SccIsMultiCheckoutEnabled 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 93cbefe716b46b3dd3fe481447612c5c7f65daa3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353575"
---
# <a name="sccismulticheckoutenabled-function"></a>SccIsMultiCheckoutEnabled 函数
此函数检查源代码管理插件是否允许多次签出文件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>参数
 pContext

[in]源控制插件上下文结构。

 pbMultiCheckout

[out]指定是否为此项目 （非零值表示，支持多个签出） 启用多个签出。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|检查成功。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 IDE 将使两个检查，以确定是否文件可以签出同时由多个用户。 首先，源代码管理系统必须支持多个签出。 源代码管理插件可以指定此功能在初始化期间通过指定`SCC_CAP_MULTICHECKOUT`。 此后，作为第二个检查中，IDE 会调用此函数可确定当前的项目支持多个签出。 如果所选项目支持多个签出，该插件返回一个成功的代码，并设置`pbMultiCheckout`不为零 (`TRUE`) 或`FALSE`。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)