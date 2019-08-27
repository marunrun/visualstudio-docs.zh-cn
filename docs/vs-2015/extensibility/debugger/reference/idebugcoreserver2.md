---
title: IDebugCoreServer2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer2
helpviewer_keywords:
- IDebugCoreServer2 interface
ms.assetid: 9c47d0a6-9eb1-464e-bd44-fa2b552d4d36
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c0bca6ccd3738518df339084b0f6463be181e52d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192914"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口用于表示，并从网络上的计算机上的服务器获取信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugCoreServer2 : IUknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 Visual Studio 实现此接口来表示一台服务器。 Visual Studio 的每个实例创建此接口的实例。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 自定义端口提供程序接收此接口的调用中[事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)。  
  
 调试引擎可以获取此接口通过调用间接[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) (它将返回[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)，派生自的接口`IDebugCoreServer2`)。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugCoreServer2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|获取名称和一台计算机的属性。|  
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|获取的计算机的名称。|  
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|获取在计算机上的端口提供程序存在。|  
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|获取计算机已存在的端口。|  
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|在计算机上创建的所有端口的枚举器。|  
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|在计算机上创建所有端口提供程序的枚举器。|  
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|获取在计算机机实用程序。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 还使用此接口来浏览网络上的计算机上运行的进程。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)   
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
