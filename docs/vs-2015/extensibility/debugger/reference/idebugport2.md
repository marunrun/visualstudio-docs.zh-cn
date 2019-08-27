---
title: IDebugPort2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPort2
helpviewer_keywords:
- IDebugPort2 interface
ms.assetid: 8fd87f05-a950-4d14-b925-98be29d4facc
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c9227e2e05499feac628a5b90fc6e3d2a4399992
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188565"
---
# <a name="idebugport2"></a>IDebugPort2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示计算机上的调试端口。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPort2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 自定义端口提供程序实现此接口来表示计算机上的调试端口。  
  
 如果端口支持将事件发送端口，它还必须实现<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>接口以支持<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>又提供接口[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)或[端口](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)返回此接口，表示请求的端口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugPort2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetPortName](../../../extensibility/debugger/reference/idebugport2-getportname.md)|返回的端口名称。|  
|[GetPortId](../../../extensibility/debugger/reference/idebugport2-getportid.md)|返回的端口标识符。|  
|[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)|返回用于创建端口 （如果可用） 的请求。|  
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)|返回此端口的端口供应商。|  
|[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)|为给定进程的标识符的过程返回的接口。|  
|[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)|枚举所有端口上运行的进程。|  
  
## <a name="remarks"></a>备注  
 本地端口提供对所有进程和在本地计算机上运行的程序的访问。 其他端口可能表示串行电缆连接到基于 Windows CE 的设备时或与非 DCOM 计算机的网络连接。 `IDebugPort2`接口用于查找的名称和标识符的一个端口，枚举的端口上运行的所有进程和提供用于启动和终止进程的端口上的工具。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
