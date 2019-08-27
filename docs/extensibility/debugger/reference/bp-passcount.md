---
title: BP_PASSCOUNT | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT
helpviewer_keywords:
- BP_PASSCOUNT structure
ms.assetid: 791ac175-b897-4c70-873e-240da7e0ac89
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3fd1ab73a20b319af6c9464062113f4e8f2d64fa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353009"
---
# <a name="bppasscount"></a>BP_PASSCOUNT
描述在其触发条件断点的计数和条件。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_PASSCOUNT {
    DWORD              dwPassCount;
    BP_PASSCOUNT_STYLE stylePassCount;
} BP_PASSCOUNT;
```

```csharp
public struct BP_PASSCOUNT {
    public uint dwPassCount;
    public uint stylePassCount;
};
```

## <a name="members"></a>成员
`dwPassCount`\
将跳过该断点之前触发它的时间数。

`stylePassCount`\
中的值[BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)枚举，用于指定断点的样式通过次数。

## <a name="remarks"></a>备注
此结构是的成员[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)结构。

此结构还作为参数传递[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)并[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)
- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)
