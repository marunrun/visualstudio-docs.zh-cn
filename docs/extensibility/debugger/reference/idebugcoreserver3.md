---
title: IDebugCoreServer3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d110e66e937249fdee34f424d4f68a9b914113d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732818"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
此接口允许访问有关进程运行中的服务器的信息。

## <a name="syntax"></a>语法

```
IDebugCoreServer3 : IDebugCoreServer2
```

## <a name="notes-for-implementers"></a>实施者说明
 可视化工作室实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 使用[查询接口](/cpp/atl/queryinterface)从[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)界面获取此接口。 对[GetServer 的](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)调用也可以返回此接口。 此接口最常由自定义端口供应商用于在服务器上启动程序（本地或远程）。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[获取服务器名称](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|检索服务器的名称。|
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|检索服务器名称的友好版本|
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|告诉特定的调试引擎在这些进程启动时自动附加到进程。|
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|自动附加失败时检索特定的错误代码。|
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|在服务器上创建调试引擎的实例。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|检索指示服务器是否与调用方位于同一台计算机上的标记。|
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|检索指示用于与服务器通信的协议的值。|
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|禁用此服务器知道的所有调试引擎的所有自动附加设置。|

## <a name="remarks"></a>备注
 自定义端口供应商在调用[事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)时接收[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)接口。 可以从`IDebugCoreServer3`该接口获取接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
