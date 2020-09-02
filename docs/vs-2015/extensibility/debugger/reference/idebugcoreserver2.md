---
title: IDebugCoreServer2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192914"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口用于在网络上的计算机上表示和获取信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugCoreServer2 : IUknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 Visual Studio 实现此接口来表示服务器。 Visual Studio 的每个实例都创建此接口的实例。  
  
## <a name="notes-for-callers"></a>调用方说明  
 自定义端口供应商在调用 [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)时接收此接口。  
  
 调试引擎可以通过对 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) (的调用间接获取此接口，该调用返回 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)，这是派生自) 的接口 `IDebugCoreServer2` 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugCoreServer2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|获取计算机的名称和属性。|  
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|获取计算机的名称。|  
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|获取计算机上存在的端口供应商。|  
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|获取计算机上已存在的端口。|  
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|为计算机上的所有端口创建枚举器。|  
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|为计算机上的所有端口供应商创建一个枚举器。|  
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|获取计算机的计算机实用程序。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 还使用此接口来浏览网络计算机上运行的进程。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [引发](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)   
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
