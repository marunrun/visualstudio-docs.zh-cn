---
title: 框架信息 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO
helpviewer_keywords:
- FRAMEINFO structure
ms.assetid: 95001b89-dddb-45bb-889d-8327994e38a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c40361a9739bf468de2038df4325fa1ac98337c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736793"
---
# <a name="frameinfo"></a>FRAMEINFO
描述堆栈帧。

## <a name="syntax"></a>语法

```cpp
typedef struct tagFRAMEINFO {
    FRAMEINFO_FLAGS    m_dwValidFields;
    BSTR               m_bstrFuncName;
    BSTR               m_bstrReturnType;
    BSTR               m_bstrArgs;
    BSTR               m_bstrLanguage;
    BSTR               m_bstrModule;
    UINT64             m_addrMin;
    UINT64             m_addrMax;
    IDebugStackFrame2* m_pFrame;
    IDebugModule2*     m_pModule;
    BOOL               m_fHasDebugInfo;
    BOOL               m_fStaleCode;
    BOOL               m_fAnnotatedFrame;
} FRAMEINFO;
```

```csharp
public struct FRAMEINFO {
    public uint              m_dwValidFields;
    public string            m_bstrFuncName;
    public string            m_bstrReturnType;
    public string            m_bstrArgs;
    public string            m_bstrLanguage;
    public string            m_bstrModule;
    public ulong             m_addrMin;
    public ulong             m_addrMax;
    public IDebugStackFrame2 m_pFrame;
    public IDebugModule2     m_pModule;
    public int               m_fHasDebugInfo;
    public int               m_fStaleCode;
    public int               m_fAnnotatedFrame;
} FRAMEINFO;
```

## <a name="members"></a>成员
`m_dwValidFields`\
[FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)枚举中的标志的组合，用于指定填充哪些字段。

`m_bstrFuncName`\
与堆栈帧关联的函数名称。

`m_bstrReturnType`\
与堆栈帧关联的返回类型。

`m_bstrArgs`\
与堆栈帧关联的函数的参数。

`m_bstrLanguage`\
实现函数的语言。

`m_bstrModule`\
与堆栈帧关联的模块名称。

`m_addrMin`\
最小物理堆栈地址。

`m_addrMAX`\
最大物理堆栈地址。

`m_pFrame`\
表示此堆栈帧的[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)对象。

`m_pModule`\
[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)对象，表示包含此堆栈帧的模块。

`m_fHasDebugInfo`\
如果给定帧中`TRUE`存在调试信息，则非零 （ ）。

`m_fStaleCode`\
如果堆栈帧`TRUE`与不再有效的代码相关联，则非零 （ ）。

`m_fAnnotatedFrame`\
如果堆栈帧`TRUE`由会话调试管理器 （SDM） 进行指示，则非零 （ ）。

## <a name="remarks"></a>备注
此结构传递给要填充的[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)方法。 此结构还包含在[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)接口中包含的列表中，该列表又从调用[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)方法返回。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
