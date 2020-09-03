---
title: BP_LOCATION_CODE_CONTEXT |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_CONTEXT
helpviewer_keywords:
- BP_LOCATION_CODE_CONTEXT structure
ms.assetid: 37412896-021a-4f73-9bb7-4125502c2e18
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 4dcb8ffb1a1debcf6aeeca8dc4d21c1ab5f18b90
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738029"
---
# <a name="bp_location_code_context"></a>BP_LOCATION_CODE_CONTEXT
描述直接绑定到正在调试的程序中的地址的断点位置。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_CODE_CONTEXT {
    IDebugCodeContext2* pCodeContext;
} BP_LOCATION_CODE_CONTEXT;
```

## <a name="members"></a>成员
`pCodeContext`\
[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，用于标识代码中断点的位置。

## <a name="remarks"></a>备注
此结构是作为联合的一部分的 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 结构的成员。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
