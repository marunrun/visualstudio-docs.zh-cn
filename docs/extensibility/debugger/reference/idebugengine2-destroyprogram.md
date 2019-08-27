---
title: IDebugEngine2::DestroyProgram | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::DestroyProgram
helpviewer_keywords:
- IDebugEngine2::DestroyProgram
ms.assetid: 0c9e2698-c70f-4770-a7bb-39650e9c3a1f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c20459329eeb9e61447c707ef6c95adf01945e5d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330078"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
通知的调试引擎 (DE) 指定的程序已异常终止，DE 应清理对该程序的所有引用和发送程序销毁事件。

## <a name="syntax"></a>语法

```cpp
HRESULT DestroyProgram( 
   IDebugProgram2* pProgram
);
```

```cpp
int DestroyProgram( 
   IDebugProgram2 pProgram
);
```

## <a name="parameters"></a>参数
`pProgram`\
[in][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示已异常终止该程序。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，随后会发送 DE [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)回会话调试管理器 (SDM) 的事件。

 未实现此方法 (返回`E_NOTIMPL`) 如果 DE 为正在调试的程序在同一进程中运行。 仅当 DE SDM 同一个进程中运行，实现此方法。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)