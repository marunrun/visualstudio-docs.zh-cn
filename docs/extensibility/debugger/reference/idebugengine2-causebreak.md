---
title: IDebugEngine2::CauseBreak |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CauseBreak
helpviewer_keywords:
- IDebugEngine2::CauseBreak
ms.assetid: 17fe4698-b04e-4798-8412-80e0da60c387
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93f9937609a09439b265946e76f0af0381d488f1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330133"
---
# <a name="idebugengine2causebreak"></a>IDebugEngine2::CauseBreak
一个其线程尝试运行所有程序 (DE) 停止执行下一次此调试引擎正在调试的请求。

## <a name="syntax"></a>语法

```cpp
HRESULT CauseBreak( 
   void 
);
```

```csharp
int CauseBreak();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法是异步的： [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)接下来，该程序尝试执行后调用此方法则会发送事件。

## <a name="see-also"></a>请参阅
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)