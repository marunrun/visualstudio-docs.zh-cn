---
title: SccGetExtendedCapabilities 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5247f2de7ffc63db7235f915c72b3274b8fee5f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700723"
---
# <a name="sccgetextendedcapabilities-function"></a>SccGetExtendedCapabilities 函数
此函数返回源代码管理插件支持的其他功能。

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

中源代码管理插件上下文指针。

 lSccExCaps

中一个标志，该标志指定要测试的扩展功能 (请参阅 [功能标志](../extensibility/capability-flags.md) 中的扩展功能代码表，查找) 的可能标志。

 pbSupported

弄 `TRUE` 如果支持指定的功能，则返回非零 () ; 否则，将返回零 (`FALSE`) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|获取功能操作已成功完成。|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|出现未知或未指定的错误。|

## <a name="remarks"></a>备注
 此方法按需调用;也就是说，当某个功能需要进行测试时，将调用此方法来确定是否支持该功能。 一次只能指定一个标志。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [错误代码](../extensibility/error-codes.md)
- [功能标志](../extensibility/capability-flags.md)
