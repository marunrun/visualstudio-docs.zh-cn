---
title: IDebugOutputStringEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2
helpviewer_keywords:
- IDebugOutputStringEvent2 interface
ms.assetid: 86596fd1-cecc-4813-8add-dc3d70068f9b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c47a920e99ece3fb0853e4e6a26dba3c8d0c45c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80726028"
---
# <a name="idebugoutputstringevent2"></a>IDebugOutputStringEvent2
此接口由调试引擎 (DE) 发送到会话调试管理器 (SDM) 以输出字符串。

## <a name="syntax"></a>语法

```
IDebugOutputStringEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口以将字符串发送到 IDE 的 " **输出** " 窗口。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以将字符串发送到 " **输出** " 窗口。 此事件在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugOutputStringEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetString](../../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)|获取可显示消息。|

## <a name="remarks"></a>备注
 例如，在非托管代码中，当正在调试的程序将字符串发送到 Win32 函数时，要输出的字符串可能产生 `OutputDebugString` 。 此字符串由 DE 截获，并作为事件发送到 SDM `IDebugOutputStringEvent2` 。

 使用 [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) 发送需要用户响应的消息。

 使用 [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) 发送不需要响应的错误消息。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
