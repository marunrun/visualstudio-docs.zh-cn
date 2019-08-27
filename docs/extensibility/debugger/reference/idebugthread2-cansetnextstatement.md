---
title: IDebugThread2::CanSetNextStatement |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::CanSetNextStatement
helpviewer_keywords:
- IDebugThread2::CanSetNextStatement
ms.assetid: 7014af80-ff4f-4790-a34b-0528918d1fa3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 111ace07edf163fa978a3c54628878af51cb7d02
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320298"
---
# <a name="idebugthread2cansetnextstatement"></a>IDebugThread2::CanSetNextStatement
确定当前指令指针是否可以设置为给定的堆栈帧。

## <a name="syntax"></a>语法

```cpp
HRESULT CanSetNextStatement ( 
   IDebugStackFrame2*  pStackFrame,
   IDebugCodeContext2* pCodeContext
);
```

```csharp
int CanSetNextStatement ( 
   IDebugStackFrame2  pStackFrame,
   IDebugCodeContext2 pCodeContext
);
```

## <a name="parameters"></a>参数
`pStackFrame`\
保留供将来使用;设置为 null 值。 如果这是一个 null 值，则使用当前堆栈帧。

`pCodeContext`\
[in][IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，描述要执行的代码位置和其上下文。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 如果此方法返回`S_OK`，然后调用[SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)方法实际上设置下一语句。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)