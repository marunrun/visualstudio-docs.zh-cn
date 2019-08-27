---
title: BP_LOCATION_RESOLUTION | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_RESOLUTION
helpviewer_keywords:
- BP_LOCATION_RESOLUTION structure
ms.assetid: 86ea2c8a-54a3-48e8-83c7-18a515273129
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: d728c0aae749caa661ae4cb8f29e13f9cd1827fb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353066"
---
# <a name="bplocationresolution"></a>BP_LOCATION_RESOLUTION
描述特定位置处的断点解决的方法。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_RESOLUTION {
    IDebugBreakpointResolution2* pResolution;
} BP_LOCATION_RESOLUTION;
```

## <a name="members"></a>成员
`pResolution`\
[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)确定断点和其解决方法信息的类型的对象。

## <a name="remarks"></a>备注
此结构是的成员[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构作为联合的一部分。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)
