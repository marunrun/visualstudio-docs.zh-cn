---
title: IDebugEngine2：:D微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::DestroyProgram
helpviewer_keywords:
- IDebugEngine2::DestroyProgram
ms.assetid: 0c9e2698-c70f-4770-a7bb-39650e9c3a1f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ce139dd22361d9914693cbe8ad723656ab7d4f26
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731106"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
通知调试引擎 （DE）， 指定的程序已终止，DE 应清除对程序的所有引用并发送程序销毁事件。

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
[在][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示已终止的程序。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，DE 随后将[IDebugProgram破坏事件2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)事件发送回会话调试管理器 （SDM）。

 如果 DE 与正在调试`E_NOTIMPL`的程序在同一进程中运行，则此方法不会实现（返回）。 仅当 DE 与 SDM 在同一进程中运行时，才会实现此方法。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
