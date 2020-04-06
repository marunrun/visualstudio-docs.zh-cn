---
title: BP_LOCATION_CODE_ADDRESS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_ADDRESS
helpviewer_keywords:
- BP_LOCATION_CODE_ADDRESS structure
ms.assetid: 83c9da8b-19d9-4be5-b225-854543654901
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: c215630e522adabdbd285e00d4bcd87cae22a931
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738036"
---
# <a name="bp_location_code_address"></a>BP_LOCATION_CODE_ADDRESS
描述代码中地址的断点位置。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_CODE_ADDRESS {
    BSTR bstrContext;
    BSTR bstrModuleUrl;
    BSTR bstrFunction;
    BSTR bstrAddress;
} BP_LOCATION_CODE_ADDRESS;
```

## <a name="members"></a>成员
`bstrContext`\
断点的上下文，通常是在调用堆栈上看到的方法或函数名称。

`bstrModuleUrl`\
包含断点的模块的 URL。

`bstrFunction`\
包含断点的函数的名称。

`bstrAddress`\
断点的地址，由表达式赋值器解析，以将其绑定到[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象。

## <a name="remarks"></a>备注
此结构是作为联合的一部分[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构的成员。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
