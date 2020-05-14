---
title: IDebugEngineProgram2：：：观看线程步骤 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf0474d527b7c6f1d180201a463f52a0b17d18fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730355"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
监视在给定线程上执行（或停止监视执行）。

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
[在][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示正在步进的程序。

`dwTid`\
[在]指定要监视的线程的标识符。

`fWatch`\
[在]非零 （）`TRUE`表示开始在 所`dwTid`标识的线程上监视执行。否则，零`FALSE`（） 表示停止监视在`dwTid`执行 。

`dwFrame`\
[在]指定控制步骤类型的帧索引。 当此值为零 （0）时，步骤类型为"进入"，每当执行标识`dwTid`的线程时，程序都应停止。 当`dwFrame`是非零时，步骤类型为"步长"，并且仅当标识`dwTid`的线程在堆栈上的索引等于或高于`dwFrame`的帧中运行时，程序才应停止。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器 （SDM） 步步由`pOriginatingProgram`参数标识的程序时，它会通过调用此方法通知所有其他附加的程序。

 此方法仅适用于同一线程步进。

## <a name="see-also"></a>请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
