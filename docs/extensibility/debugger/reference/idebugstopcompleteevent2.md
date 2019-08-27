---
title: IDebugStopCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d080b3073ffc13b90870b40a16a353634f4aa0cf
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352009"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2

程序已停止时，调试引擎 (DE) 可以向会话调试管理器 (SDM) 发送此可选事件。

## <a name="syntax"></a>语法

```
IDebugStopCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明

使用 Visual Studio 2005 引入了此接口。 以前的版本不支持异步停止。

- [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)SDM 在多进程或多程序的情况下调用。 当一个程序将停止事件发送到 SDM 时，SDM 请求停止，过其他程序。

停止用于异步通知程序已经停止 SDM。 通知 SDM 可用于解释器调试引擎，其中有时不运行任何代码在调试程序，这样[停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)未以同步方式完成。 如果调试引擎想要使用此异步通知时，它必须返回`S_ASYNC_STOP`从[停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)。

## <a name="requirements"></a>要求

标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll