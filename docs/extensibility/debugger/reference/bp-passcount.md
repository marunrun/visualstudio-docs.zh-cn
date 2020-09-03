---
title: BP_PASSCOUNT |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT
helpviewer_keywords:
- BP_PASSCOUNT structure
ms.assetid: 791ac175-b897-4c70-873e-240da7e0ac89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e3177ff093aea9a6f52465bd606b22883249d6b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737912"
---
# <a name="bp_passcount"></a>BP_PASSCOUNT
描述触发条件断点的计数和条件。

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
在引发断点之前传递该断点的次数。

`stylePassCount`\
[BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)枚举中的一个值，该值指定断点传递计数的样式。

## <a name="remarks"></a>备注
此结构是 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 结构的成员。

此结构也作为参数传递给[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md) 和[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md) 方法。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)
- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)
