---
title: IDebugProgram2：：枚举代码路径 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b99651811cedbdb8ec0eca5b766e6d75651dd5d7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723029"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
检索源文件中给定位置的代码路径列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumCodePaths( 
   LPCOLESTR            pszHint,
   IDebugCodeContext2*  pStart,
   IDebugStackFrame2*   pFrame,
   BOOL                 fSource,
   IEnumCodePaths2**    ppEnum,
   IDebugCodeContext2** ppSafety
);
```

```csharp
int EnumCodePaths( 
   string                 pszHint,
   IDebugCodeContext2     pStart,
   IDebugStackFrame2      pFrame,
   Int                    fSource,
   out IEnumCodePaths2    ppEnum,
   out IDebugCodeContext2 ppSafety
);
```

## <a name="parameters"></a>参数
`pszHint`\
[在]IDE 中的 **"源**"或"**拆解**"视图中光标下方的单词。

`pStart`\
[在]表示当前代码上下文的[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象。

`pFrame`\
[在][IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)对象，表示与当前断点关联的堆栈帧。

`fSource`\
[在]非零`TRUE`（ ） 如果位于 **"源"** 视图中`FALSE`，则为零 （） （）， 如果在 **"拆解"** 视图中。

`ppEnum`\
[出]返回包含代码路径列表的[IEnumCodePath2](../../../extensibility/debugger/reference/ienumcodepaths2.md)对象。

`ppSafety`\
[出]返回一个[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，表示要设置为断点的其他代码上下文，以防跳过所选代码路径。 例如，在短路布尔表达式的情况下，可能会发生这种情况。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 代码路径描述为在程序执行中到达当前点而调用的方法或函数的名称。 代码路径列表表示调用堆栈。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
