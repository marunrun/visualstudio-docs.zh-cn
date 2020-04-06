---
title: IDebug消息事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2
helpviewer_keywords:
- IDebugMessageEvent2 interface
ms.assetid: a9ff3d00-e9ac-4cd6-bda9-584a4815aff8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 180162988cbb09f98b7fc2e8f33f6b5d0ed322ae
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727360"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
调试引擎 （DE） 使用此接口向 Visual Studio 发送消息，该消息需要用户响应。

## <a name="syntax"></a>语法

```
IDebugMessageEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以向需要用户响应的 Visual Studio 发送消息。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现。 SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

 此接口的实现必须将 Visual Studio 的[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)调用传达给 DE。 例如，这可以通过发布到 DE 的消息处理线程的消息来完成，或者实现此接口的对象可以保留对 DE 的引用，并在将响应传递到`IDebugMessageEvent2::SetResponse`下调用 DE。

## <a name="notes-for-callers"></a>呼叫者备注
 DE 创建并发送此事件对象以向需要响应的用户显示消息。 该事件使用 SDM 在附加到正在调试的程序时提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调函数进行发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugMessageEvent2`。

|方法|描述|
|------------|-----------------|
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|获取要显示的消息。|
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|从消息框中设置响应（如果有）。|

## <a name="remarks"></a>备注
 如果 DE 需要用户对特定消息的特定响应，则 DE 将使用此接口。 例如，如果 DE 在尝试远程附加到程序后收到"访问被拒绝"消息，则 DE 在具有消息框样式`IDebugMessageEvent2``MB_RETRYCANCEL`的事件中将此特定消息发送到 Visual Studio。 这允许用户重试或取消附加操作。

 DE 指定如何按照 Win32 函数`MessageBox`的约定处理此消息（有关详细信息，请参阅[AfxMessageBox）。](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)

 使用[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)界面向不需要用户响应的 Visual Studio 发送消息。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
