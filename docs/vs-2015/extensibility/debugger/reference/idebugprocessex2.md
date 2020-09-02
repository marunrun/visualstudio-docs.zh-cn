---
title: IDebugProcessEx2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcessEx2
helpviewer_keywords:
- IDebugProcessEx2 interface
ms.assetid: 44e309ba-1d6f-499b-aa7e-9b34858a6d57
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d2b036bd68aca126675f26b9823d2c786a0ae652
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675333"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口使会话调试管理器 (SDM) 通知它附加到进程或从进程分离的进程。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProcessEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 自定义端口供应商在与 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 接口相同的对象上实现此接口，以便：  
  
- 支持跟踪连接到进程的会话  
  
- 支持跨多个调试引擎自动附加  
  
  自定义端口供应商可以在选择的情况下实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
  
- SDM 在接口[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上调用 QueryInterface `IDebugProcess2` 以获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugProcessEx2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[附加](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|通知进程会话正在调试该进程。|  
|[分离](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|通知进程：会话不再调试该进程。|  
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|为调试引擎列表添加程序节点。|  
  
## <a name="remarks"></a>备注  
 此接口在 SDM 和进程之间是私有的。  
  
## <a name="requirements"></a>要求  
 标头： Portpriv  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
