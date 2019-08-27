---
title: IDebugInterceptExceptionCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2
ms.assetid: 8ebc256b-5428-4ed6-a505-6aedc8242b8e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 847565b4e0e1f3e8d9a19f6572531834197b39ac
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349479"
---
# <a name="idebuginterceptexceptioncompleteevent2"></a>IDebugInterceptExceptionCompleteEvent2
DE 完成后被拦截事件的处理，此接口是由调试引擎 (DE) 发送到会话调试管理器 (SDM) 中。

## <a name="syntax"></a>语法

```
IDebugInterceptExceptionCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口以报告已完成的已截获异常处理。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建并发送此事件对象来报告已完成已截获异常。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 `IDebugInterceptExceptionCompleteEvent2`接口实现以下方法。

|方法|描述|
|------------|-----------------|
|[GetInterceptCookie](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2-getinterceptcookie.md)|返回与已处理的异常关联的唯一值。|

## <a name="remarks"></a>备注
 此事件将发送[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)时该方法已成功地处理已截获的异常。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)