---
title: IDebugPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2
helpviewer_keywords:
- IDebugPort2 interface
ms.assetid: 8fd87f05-a950-4d14-b925-98be29d4facc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62912be9fdfecc98a264a58c9713cc12ccaf28f2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80725228"
---
# <a name="idebugport2"></a>IDebugPort2
此接口表示计算机上的调试端口。

## <a name="syntax"></a>语法

```
IDebugPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 自定义端口供应商实现此接口，以表示计算机上的调试端口。

 如果端口支持发送端口事件，则它还必须实现 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> 接口以支持 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> 接口，进而提供 [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) 接口。

## <a name="notes-for-callers"></a>调用方说明
 对 [GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md) 或 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 的调用返回此接口，表示请求的端口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugPort2` 。

|方法|说明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugport2-getportname.md)|返回端口名称。|
|[GetPortId](../../../extensibility/debugger/reference/idebugport2-getportid.md)|返回端口标识符。|
|[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)|如果可用) ，则返回用于创建端口 (的请求。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)|返回此端口的端口供应商。|
|[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)|返回给定进程标识符的进程的接口。|
|[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)|枚举端口上运行的所有进程。|

## <a name="remarks"></a>备注
 本地端口提供对本地计算机上运行的所有进程和程序的访问权限。 其他端口可能代表到基于 Windows CE 的设备的串行电缆连接，或与非 DCOM 计算机的网络连接。 `IDebugPort2`接口用于查找端口的名称和标识符，并枚举端口上运行的所有进程。 用于启动和终止端口上的进程的功能是在接口中实现的 `IDebugPortEx2` 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
