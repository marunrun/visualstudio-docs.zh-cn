---
title: EXCEPTION_INFO |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_INFO
helpviewer_keywords:
- EXCEPTION_INFO structure
ms.assetid: d046957a-b97d-420b-b46b-c67cbaef709e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a305d34123d02b1fdbd545a438db4461643ed185
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737030"
---
# <a name="exception_info"></a>EXCEPTION_INFO
描述正在调试的程序引发的异常或运行时错误。

## <a name="syntax"></a>语法

```cpp
typedef struct tagEXCEPTION_INFO {
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    BSTR            bstrExceptionName;
    DWORD           dwCode;
    EXCEPTION_STATE dwState;
    GUID            guidType;
} EXCEPTION_INFO;
```

```csharp
public struct EXCEPTION_INFO {
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public string         bstrExceptionName;
    public uint           dwCode;
    public uint           dwState;
    public Guid           guidType;
};
```

## <a name="members"></a>成员
`pProgram`\
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示发生异常的程序。

`bstrProgramName`\
发生异常的程序的名称。

`bstrExceptionName`\
异常的名称。

`dwCode`\
异常或运行时错误的标识代码。

`dwState`\
定义异常状态[EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)枚举的值。

`guidType`\
GUID 语言标识符（或`guidLang``guidEng`"

## <a name="remarks"></a>备注
此结构作为参数传递给[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)和[RemoveSetexception](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)方法。 此结构也会传递到要填充的[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)方法。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
- [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)
