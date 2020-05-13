---
title: IDebugStop完成事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: da3eb33d76f55310e6428a34dd09cabbc271aa68
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719441"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2

当程序停止时，调试引擎 （DE） 可以将此可选事件发送到会话调试管理器 （SDM）。

## <a name="syntax"></a>语法

```
IDebugStopCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明

此接口是使用 Visual Studio 2005 引入的。 以前的版本不支持异步停止。

- 在多进程或多程序方案中，SDM 调用[Stop。](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) 当一个程序向 SDM 发送停止事件时，SDM 也会请求其他程序停止。

停止用于异步通知 SDM 程序已停止。 通知 SDM 对于解释器调试引擎很有用，有时调试程序中没有代码运行，因此[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)无法同步完成。 如果调试引擎想要使用此异步通知，它必须从[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)返回`S_ASYNC_STOP`。

## <a name="requirements"></a>要求

标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll
