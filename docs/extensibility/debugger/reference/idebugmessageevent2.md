---
title: IDebugMessageEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2
helpviewer_keywords:
- IDebugMessageEvent2 interface
ms.assetid: a9ff3d00-e9ac-4cd6-bda9-584a4815aff8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: facb0b818ab8bd8babae59e6cdbd2b209a8cfda7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346836"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
此接口由调试引擎 (DE) 用于将消息发送到需要来自用户的响应的 Visual Studio。

## <a name="syntax"></a>语法

```
IDebugMessageEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口以将消息发送到需要用户响应的 Visual Studio。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

 此接口的实现必须进行通信的 Visual Studio 调用[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)到德国。 例如，这可以通过一条消息发送到设备的消息处理线程，或实现此接口的对象无法保存对 DE 的引用并调用回 DE 与传递到响应`IDebugMessageEvent2::SetResponse`。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建并发送此事件对象需要一个响应的用户显示一条消息。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 附加到正在调试的程序时提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugMessageEvent2`。

|方法|描述|
|------------|-----------------|
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|获取要显示的消息。|
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|设置响应中，如果有，该消息框中。|

## <a name="remarks"></a>备注
 如果某个特定消息需要来自用户的特定响应，DE 将使用此接口。 例如，如果 DE 后尝试远程附加到程序中获取的"拒绝访问"消息，DE 此特定将消息发送到 Visual Studio 中的`IDebugMessageEvent2`事件和消息框样式`MB_RETRYCANCEL`。 这允许用户重试或取消附加操作。

 DE 指定由以下 Win32 函数的约定来处理此消息的方式`MessageBox`(请参阅[AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)有关详细信息)。

 使用[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)接口以便将消息发送到不需要来自用户的响应的 Visual Studio。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)