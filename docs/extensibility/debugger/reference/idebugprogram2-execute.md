---
title: IDebugProgram2：：执行 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Execute
helpviewer_keywords:
- IDebugProgram2::Execute
ms.assetid: f7205ce8-0ac6-4fcd-b6ec-b720b4fcaccf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f34ebea67ff95d1da6d777cdd828604f4a2f56e8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722979"
---
# <a name="idebugprogram2execute"></a>IDebugProgram2::Execute
继续从已停止状态运行此程序。 清除任何以前的执行状态（如步骤），程序将再次开始执行。

> [!NOTE]
> 不推荐使用此方法。 请改用[Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)方法。

## <a name="syntax"></a>语法

```cpp
HRESULT Execute(
   void
);
```

```csharp
int Execute();
```

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 当用户从其他程序线程中的停止状态开始执行时，此程序将调用此方法。 当用户从 IDE 中的 **"调试"** 菜单中选择 **"开始"** 命令时，也会调用此方法。 此方法的实现可能很简单，如在程序中的当前线程上调用[Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)方法。

> [!WARNING]
> 在处理此调用时，不要向[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送停止事件或立即（同步）事件;否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)
