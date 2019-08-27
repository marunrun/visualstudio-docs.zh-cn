---
title: IDebugProgram2::EnumCodePaths |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3206a9c89197ccc9415115fe9fb0995e51ede8c9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353186"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
检索在源文件中的给定位置的代码路径的列表。

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
[in]中光标下的词**源**或**反汇编**在 IDE 中的视图。

`pStart`\
[in][IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，表示当前代码上下文。

`pFrame`\
[in][IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)对象与当前断点表示堆栈帧关联。

`fSource`\
[in]非零值 (`TRUE`) 中的 if**源**视图中，则为零 (`FALSE`) 中的 if**反汇编**视图。

`ppEnum`\
[out]返回[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)对象，其中包含一系列代码路径。

`ppSafety`\
[out]返回[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象表示在所选的代码路径的情况下，作为断点设置额外的代码上下文，将跳过。 发生这种情况对于短路的布尔表达式，例如。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 代码路径，用于描述方法或函数的调用以获取执行程序中的当前点的名称。 一系列代码路径表示调用堆栈。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)