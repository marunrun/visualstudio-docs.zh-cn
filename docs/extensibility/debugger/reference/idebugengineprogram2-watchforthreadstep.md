---
title: IDebugEngineProgram2::WatchForThreadStep |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6b3f8db95d6e74a2aa1d146bdd37a66803a8503f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345147"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
监视是否执行 （或停止监视执行） 的给定线程上发生。

## <a name="syntax"></a>语法

```cpp
HRESULT WatchForThreadStep( 
   IDebugProgram2* pOriginatingProgram,
   DWORD           dwTid,
   BOOL            fWatch,
   DWORD           dwFrame
);
```

```csharp
int WatchForThreadStep( 
   IDebugProgram2 pOriginatingProgram,
   uint           dwTid,
   int            fWatch,
   uint           dwFrame
);
```

## <a name="parameters"></a>参数
`pOriginatingProgram`\
[in][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示正在单步执行程序。

`dwTid`\
[in]指定要监视的线程标识符。

`fWatch`\
[in]非零 (`TRUE`) 表示开始观看由标识的线程上执行`dwTid`; 否则为零 (`FALSE`) 方法停止执行上观看`dwTid`。

`dwFrame`\
[in]指定一个帧索引，它控制的步骤类型。 在这种值为零 (0)、 步骤类型是"单步执行"和线程标识时，应停止该程序`dwTid`执行。 当`dwFrame`为非零，步骤类型是"逐过程"，并且仅当线程标识，该程序应停止`dwTid`中的索引是等于或更高版本上比堆栈帧运行`dwFrame`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器 (SDM) 步骤的程序，由标识`pOriginatingProgram`参数，它通过调用此方法通知所有其他附加的程序。

 此方法是仅适用于单步执行同一个线程。

## <a name="see-also"></a>请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)