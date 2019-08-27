---
title: IDebugCoreServer3 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cd1781b133b4c3ee95b4207a0dd237e2dd7298a1
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685652"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口可以访问的服务器进程正在运行中的相关信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugCoreServer3 : IDebugCoreServer2  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 Visual Studio 实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)若要获取此接口从[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)接口。 调用[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)还可以返回此接口。 此接口是最常用的自定义端口提供程序以启动服务器 （本地或远程） 上的程序。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了上的方法[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|检索服务器的名称。|  
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|检索服务器名称的友好版本|  
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|指示特定的调试引擎以这些进程启动时自动附加到进程。|  
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|检索特定的错误代码时自动附加失败。|  
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|在服务器上创建调试引擎的实例。|  
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|检索一个标志，指示服务器是否作为调用方在同一台计算机上。|  
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|检索一个值，该值用于与服务器通信的协议。|  
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|禁用所有自动都附加此服务器就知道有关的所有调试引擎的设置。|  
  
## <a name="remarks"></a>备注  
 自定义端口供应商接收[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)接口上调用[事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)。 `IDebugCoreServer3`接口可以获取从该接口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)   
 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
