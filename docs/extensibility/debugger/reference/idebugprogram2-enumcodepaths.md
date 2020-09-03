---
title: IDebugProgram2：： EnumCodePaths |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723029"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
检索源文件中给定位置的代码路径的列表。

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
中IDE 中的 " **源** " 或 " **反汇编** " 视图中光标下的单词。

`pStart`\
中表示当前代码上下文的 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。

`pFrame`\
中一个 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 对象，表示与当前断点关联的堆栈帧。

`fSource`\
中 `TRUE` 如果在 " **源** " 视图中，则为非零 () ，或者 `FALSE` 在 " **反汇编** " 视图中 () 。

`ppEnum`\
弄返回一个 [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md) 对象，该对象包含代码路径的列表。

`ppSafety`\
弄返回一个 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象，该对象表示要在跳过所选代码路径时设置为断点的附加代码上下文。 例如，在短路布尔表达式的情况下可能会发生这种情况。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 代码路径描述了为获取程序执行中的当前点而调用的方法或函数的名称。 代码路径列表表示调用堆栈。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
