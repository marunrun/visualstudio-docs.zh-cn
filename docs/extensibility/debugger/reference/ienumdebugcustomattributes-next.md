---
title: IEnum调试自定义属性：：下一个 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::Next
helpviewer_keywords:
- IEnumDebugCustomAttributes::Next
ms.assetid: e36f856b-2619-42d1-b73e-4f2390fc22bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08228fe4a630eac37c38f4eb247dc91678d8e2e2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717233"
---
# <a name="ienumdebugcustomattributesnext"></a>IEnumDebugCustomAttributes::Next
检索枚举序列中指定数量的自定义属性。

## <a name="syntax"></a>语法

```cpp
HRESULT Next ( 
   ULONG      celt,
   CODE_PATH* rgelt,
   ULONG*     pceltFetched
);
```

```csharp
int Next(
   uint                        celt,
   out IDebugCustomAttribute[] rgelt,
   ref uint                    pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[在]要检索的元素数。 还指定`rgelt`数组的最大大小。

`rgelt`\
[出]要填充的[IDebugCustom属性](../../../extensibility/debugger/reference/idebugcustomattribute.md)对象的数组。

`pceltFetched`\
[出]返回 中`rgelt`实际返回的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果`S_FALSE`返回的元素数少于请求的元素数，则返回;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
