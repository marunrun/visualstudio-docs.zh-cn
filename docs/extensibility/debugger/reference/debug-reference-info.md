---
title: DEBUG_REFERENCE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REFERENCE_INFO
helpviewer_keywords:
- DEBUG_REFERENCE_INFO structure
ms.assetid: 24b83d00-d756-42a1-8083-730f998761dc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c22ab1a7d0cb03f66455f76c1d9878a9df76604e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346133"
---
# <a name="debugreferenceinfo"></a>DEBUG_REFERENCE_INFO
描述的引用。

## <a name="syntax"></a>语法

```cpp
typedef struct tagDEBUG_REFERENCE_INFO {
    DEBUGREF_INFO_FLAGS dwFields;
    BSTR                bstrName;
    BSTR                bstrType;
    BSTR                bstrValue;
    DBG_ATTRIB_FLAGS    dwAttrib;
    REFERENCE_TYPE.     dwRefType;
    IDebugReference2*   m_pReference;
} DEBUG_REFERENCE_INFO;
```

```csharp
public struct DEBUG_REFERENCE_INFO {
    public uint             dwFields;
    public string           bstrName;
    public string           bstrType;
    public string           bstrValue;
    public ulong            dwAttrib;
    public uint.            dwRefType;
    public IDebugReference2 m_pReference;
};
```

## <a name="members"></a>成员
`dwFields`\
中的标志的组合[DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)枚举，用于指定哪些字段填写。

`bstrName`\
用户指定的名称[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象。

`bstrType`\
形式的格式化字符串的引用类型。

`bstrValue`\
形式的格式化字符串的引用值

`dwAttrib`\
中的标志的组合[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)指定调试属性特性的标志的枚举。

`dwRefType`\
中的值[REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)枚举，用于指定引用类型是强还是弱。

`m_pReference`\
[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象，它指定的参考信息。

## <a name="remarks"></a>备注
此结构传递给调用[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)要填充的方法。 从列表的一部分，也会返回此结构[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)接口，反过来，通过调用将返回该值[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
