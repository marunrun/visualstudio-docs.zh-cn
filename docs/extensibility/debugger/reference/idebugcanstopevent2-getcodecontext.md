---
title: IDebugCanStopEvent2::GetCodeContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetCodeContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetCodeContext
ms.assetid: eecf08b6-f9b7-4358-941b-3a448a92ac62
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3f5b43a685bcaadccdac1d12ffce2df578a842ee
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350094"
---
# <a name="idebugcanstopevent2getcodecontext"></a>IDebugCanStopEvent2::GetCodeContext
获取用于描述此事件的位置的代码上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCodeContext( 
   IDebugCodeContext2** ppCodeContext
);
```

```csharp
int GetCodeContext( 
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>参数
`ppCodeContext`\
[out]返回[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，表示当前的代码位置。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 为大多数运行时体系结构，代码上下文可以认为的在程序的执行流中，指向特定指令的地址。

 若要获取的文档上下文，这是面向源代码的行，调用[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)