---
title: SccGetExtendedCapabilities 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa6a067a0b9e8358f503228dbc53e20586b84468
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353671"
---
# <a name="sccgetextendedcapabilities-function"></a>SccGetExtendedCapabilities 函数
此函数返回受源代码管理插件的其他功能。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetExtendedCapabilities(
   LPVOID pContext,
   LONG lSccExCaps,
   LPBOOL pbSupported
);
```

### <a name="parameters"></a>参数
 pContext

[in]源控件插件上下文指针。

 lSccExCaps

[in]标志，指定对其进行测试的扩展的功能 (请参阅中的扩展功能代码表[功能标志](../extensibility/capability-flags.md)可能标志)。

 pbSupported

[out]返回非零值 (`TRUE`) 如果支持指定的功能; 否则，返回零 (`FALSE`)。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|获取功能操作已成功完成。|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|出现未知或未指定错误。|

## <a name="remarks"></a>备注
 按需; 调用此方法也就是说，当一项功能需要进行测试，调用此方法是可确定是否支持功能。 指定一次只有一个标志。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [错误代码](../extensibility/error-codes.md)
- [功能标志](../extensibility/capability-flags.md)