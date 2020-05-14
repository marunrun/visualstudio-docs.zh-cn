---
title: IDebugPort2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725228"
---
# <a name="idebugport2"></a>IDebugPort2
此接口表示计算机上的调试端口。

## <a name="syntax"></a>语法

```
IDebugPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商实现此接口以表示计算机上的调试端口。

 如果端口支持发送端口事件，它还必须实现<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>接口以支持接口，该<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>接口反过来提供[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)接口。

## <a name="notes-for-callers"></a>呼叫者备注
 对[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)或[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)的调用返回此接口，表示请求的端口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugPort2`。

|方法|描述|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugport2-getportname.md)|返回端口名称。|
|[GetPortId](../../../extensibility/debugger/reference/idebugport2-getportid.md)|返回端口标识符。|
|[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)|返回用于创建端口的请求（如果可用）。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)|返回此端口的端口供应商。|
|[获取过程](../../../extensibility/debugger/reference/idebugport2-getprocess.md)|返回进程接口，给定进程的标识符。|
|[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)|枚举在端口上运行的所有进程。|

## <a name="remarks"></a>备注
 本地端口提供对本地计算机上运行的所有进程和程序的访问。 其他端口可能表示与基于 Windows CE 的设备的串行电缆连接，或与非 DCOM 计算机的网络连接。 接口`IDebugPort2`用于查找端口的名称和标识符，并枚举在端口上运行的所有进程。 在`IDebugPortEx2`接口中实现了在端口上启动和终止进程的设施。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
