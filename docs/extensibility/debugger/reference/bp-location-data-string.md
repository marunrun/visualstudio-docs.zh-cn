---
title: BP_LOCATION_DATA_STRING |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_DATA_STRING
helpviewer_keywords:
- BP_LOCATION_DATA_STRING structure
ms.assetid: 445d6f3f-95b0-47ac-85e2-51b778240687
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 75f881feaaa2068abd98d771a63024f20435d98f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737967"
---
# <a name="bp_location_data_string"></a>BP_LOCATION_DATA_STRING
用于设置基于用户可以从集成开发环境 （IDE） 输入的字符串的数据断点。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_DATA_STRING {
    IDebugThread2* pThread;
    BSTR           bstrContext;
    BSTR           bstrDataExpr;
    DWORD          dwNumElements;
} BP_LOCATION_DATA_STRING;
```

## <a name="members"></a>成员
`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示发生断点的线程。

`bstrContext`\
代码中的断点的上下文，通常是调用堆栈上看到的方法或函数名称。

`bstrDataExpr`\
用户输入的数据字符串来设置断点。

`dwNumElements`\
发生断点的数据字符串中的元素数。

## <a name="remarks"></a>备注
此结构是作为联合的一部分[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构的成员。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
