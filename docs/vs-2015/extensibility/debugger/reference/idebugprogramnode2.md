---
title: IDebugProgramNode2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNode2
helpviewer_keywords:
- IDebugProgramNode2 interface
ms.assetid: 80e511d8-9b40-4a85-aa5d-952fa5ee6ae7
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1188f18e4a6f604dfd82991433bc0ffe0a07ad47
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148562"
---
# <a name="idebugprogramnode2"></a>IDebugProgramNode2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示可调试的程序。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProgramNode2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 或自定义端口提供程序实现此接口来表示可调试的程序。 此接口通常实现上实现的相同对象[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口。 此接口与注册[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]通过调用[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)返回此接口。 自定义端口供应商接收通过调用此接口[AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)。 DE 接收通过调用此接口[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugProgramNode2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetProgramName](../../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)|获取程序的名称。|  
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)|获取托管程序的进程的名称。|  
|[GetHostPid](../../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)|获取托管程序的进程的系统进程标识符。|  
|[GetHostMachineName_V7](../../../extensibility/debugger/reference/idebugprogramnode2-gethostmachinename-v7.md)|不推荐使用。 不要使用。|  
|[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)|不推荐使用。 不要使用。 请参阅[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)另一种方法的接口。|  
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)|获取名称和运行此程序 DE 的标识符。|  
|[DetachDebugger_V7](../../../extensibility/debugger/reference/idebugprogramnode2-detachdebugger-v7.md)|不推荐使用。 不要使用。|  
  
## <a name="remarks"></a>备注  
 会话调试管理器 (SDM) 通常会调用[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)若要获取此接口。  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)   
 [RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)   
 [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)   
 [PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)
