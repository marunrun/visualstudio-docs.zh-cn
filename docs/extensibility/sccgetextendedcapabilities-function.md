---
title: SccGet 扩展功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700723"
---
# <a name="sccgetextendedcapabilities-function"></a>SccGet 扩展功能功能
此功能返回源代码管理插件支持的其他功能。

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

[在]源代码管理插件上下文指针。

 lSccExCaps

[在]指定要测试的扩展功能的标志（请参阅["功能"标志](../extensibility/capability-flags.md)中的扩展功能代码表，了解可能的标志）。

 pb 支持

[出]如果支持指定的功能，`TRUE`则返回非零 （ ），否则，返回零`FALSE`（）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|获取功能操作已成功完成。|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|发生未知或未指定的错误。|

## <a name="remarks"></a>备注
 此方法是按需调用的;也就是说，当需要测试功能时，将调用此方法以确定该功能是否受支持。 一次只指定一个标志。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [错误代码](../extensibility/error-codes.md)
- [功能标志](../extensibility/capability-flags.md)
