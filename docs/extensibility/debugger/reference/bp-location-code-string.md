---
title: BP_LOCATION_CODE_STRING |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_STRING
helpviewer_keywords:
- BP_LOCATION_CODE_STRING structure
ms.assetid: a4cd71c6-5052-45fe-907b-ebc6ca1df2e4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 0fc0d9a053faf69fde500333ab0faafa0e8d3448
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737980"
---
# <a name="bp_location_code_string"></a>BP_LOCATION_CODE_STRING
用于根据用户可以从集成开发环境 （IDE） 输入的字符串设置代码断点。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_CODE_STRING {
    BSTR bstrContext;
    BSTR bstrCodeExpr;
} BP_LOCATION_CODE_STRING;
```

## <a name="members"></a>成员
`bstrContext`\
代码中的断点的上下文，通常是调用堆栈上看到的方法或函数名称。

`bstrCodeExpr`\
用户键入以描述代码断点的字符串。

## <a name="remarks"></a>备注
此结构是作为联合的一部分[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构的成员。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
