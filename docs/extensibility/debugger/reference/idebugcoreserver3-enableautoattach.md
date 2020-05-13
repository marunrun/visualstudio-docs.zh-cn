---
title: IDebugCoreServer3：：启用自动连接 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::EnableAutoAttach
helpviewer_keywords:
- IDebugCoreServer3::EnableAutoAttach
ms.assetid: 06aa633b-263b-4e08-8844-9a52d5120b94
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d529bb80f79a3f2972e9349a2679bb528cc10463
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732912"
---
# <a name="idebugcoreserver3enableautoattach"></a>IDebugCoreServer3::EnableAutoAttach
启用指定调试引擎的自动连接。

## <a name="syntax"></a>语法

```cpp
HRESULT EnableAutoAttach(
   GUID*     rgguidSpecificEngines,
   DWORD     celtSpecificEngines,
   LPCOLESTR pszStartPageUrl,
   BSTR*     pbstrSessionId
);
```

```csharp
int EnableAutoAttach(
   Guid[]     rgguidSpecificEngines,
   uint       celtSpecificEngines,
   string     pszStartPageUrl,
   out string pbstrSessionId
);
```

## <a name="parameters"></a>参数
`rgguidSpecificEngines`\
[在]每个调试引擎的 GUID 数组，以标记为自动附加。

`celtSpecificEngines`\
[在]中`rgguidSpecificEngines`指定的引擎数。

`pszStartPageUrl`\
[在]自动附加时要使用的起始 URL。

`pbstrSessionID`\
[出]自动连接的会话的 ID。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。 一个错误代码是`E_AUTO_ATTACH_NOT_REGISTERED`，它指示自动附加类工厂尚未注册。

## <a name="remarks"></a>备注
 启动与指定 URL 关联的程序时，将自动启动并附加指定的调试引擎。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
