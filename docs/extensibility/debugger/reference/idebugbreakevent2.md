---
title: IDebugBreakevent2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1af6ce13de529fef5e16b3bc1be7053f0e1347b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735401"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
此接口告诉会话调试管理器 （SDM） 已成功完成异步中断。

## <a name="syntax"></a>语法

```
IDebugBreakEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以支持程序中的用户中断。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现（SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口）。

## <a name="notes-for-callers"></a>呼叫者备注
 当用户请求暂停正在调试的程序时，SDM 将调用["原因中断](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)"。 成功暂停程序后，DE 将发送事件`IDebugBreakEvent2`。 此事件使用 SDM 提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调功能在附加到正在调试的程序时发送。

## <a name="remarks"></a>备注
 例如，用户可以在 **"调试"** 菜单上选择 **"全部中断"** 命令，以从运行无限循环的程序中断开。 SDM 通过调用["原因中断](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)"告诉程序停止。 当程序最终`IDebugBreakEvent2`停止时，DE 发送。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
