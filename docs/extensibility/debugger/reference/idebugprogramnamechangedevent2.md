---
title: IDebugProgramNameChangedEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramNameChangedEvent2 interface
ms.assetid: be1f1cd5-0b2f-435c-a052-dca28a7c978d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ae58728601c3adbe6e37a00fd0694a5d71eef0b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722146"
---
# <a name="idebugprogramnamechangedevent2"></a>IDebugProgramNameChangedEvent2
当程序的名称更改时，从调试引擎发送 (取消) 到会话调试管理器 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugProgramNameChangedEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口，报告程序的名称已更改。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 **IDebugEvent2** 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以报告程序名称更改。 DE 在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送此事件。 自定义端口供应商使用 I 接口发送此事件。

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
