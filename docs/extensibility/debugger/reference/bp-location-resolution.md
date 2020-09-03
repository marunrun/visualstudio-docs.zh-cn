---
title: BP_LOCATION_RESOLUTION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_RESOLUTION
helpviewer_keywords:
- BP_LOCATION_RESOLUTION structure
ms.assetid: 86ea2c8a-54a3-48e8-83c7-18a515273129
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 5f33f01d0c2b8465bbb417b56576118349234970
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737955"
---
# <a name="bp_location_resolution"></a>BP_LOCATION_RESOLUTION
描述特定位置的断点解析。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_RESOLUTION {
    IDebugBreakpointResolution2* pResolution;
} BP_LOCATION_RESOLUTION;
```

## <a name="members"></a>成员
`pResolution`\
确定断点类型及其解决方法信息的 [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md) 对象。

## <a name="remarks"></a>备注
此结构是作为联合的一部分的 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 结构的成员。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)
