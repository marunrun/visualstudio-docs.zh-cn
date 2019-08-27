---
title: BP_LOCATION_CODE_CONTEXT | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_CONTEXT
helpviewer_keywords:
- BP_LOCATION_CODE_CONTEXT structure
ms.assetid: 37412896-021a-4f73-9bb7-4125502c2e18
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 95d09c81fa12e6f06157aeb28aa6b1837f95009e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353084"
---
# <a name="bplocationcodecontext"></a>BP_LOCATION_CODE_CONTEXT
介绍了直接绑定到正在调试的程序中的一个地址断点的位置。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_CODE_CONTEXT {
    IDebugCodeContext2* pCodeContext;
} BP_LOCATION_CODE_CONTEXT;
```

## <a name="members"></a>成员
`pCodeContext`\
[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，用于标识在代码中的断点的位置。

## <a name="remarks"></a>备注
此结构是的成员[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构作为联合的一部分。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
