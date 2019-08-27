---
title: IDebugOutputStringEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2
helpviewer_keywords:
- IDebugOutputStringEvent2 interface
ms.assetid: 86596fd1-cecc-4813-8add-dc3d70068f9b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d47fe2b329f9f2fb4adb57cdf6e2a6a871299d14
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311902"
---
# <a name="idebugoutputstringevent2"></a>IDebugOutputStringEvent2
此接口是由发送调试引擎 (DE) 会话调试管理器 (SDM) 以输出一个字符串。

## <a name="syntax"></a>语法

```
IDebugOutputStringEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口以发送到的字符串**输出**在 IDE 的窗口。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建，并将此事件的对象将字符串发送到发送**输出**窗口。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 附加到正在调试的程序时提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugOutputStringEvent2`。

|方法|描述|
|------------|-----------------|
|[GetString](../../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)|获取可显示的消息。|

## <a name="remarks"></a>备注
 例如，在非托管代码中，可以源自要输出的字符串，当正在调试的程序将字符串发送到 Win32`OutputDebugString`函数。 此字符串是由 DE 截获和日志发送到作为 SDM`IDebugOutputStringEvent2`事件。

 使用[IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)发送一条消息，需要用户响应。

 使用[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)发送错误消息，不需要进行响应。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)