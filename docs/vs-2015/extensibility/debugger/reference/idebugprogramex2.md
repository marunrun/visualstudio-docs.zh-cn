---
title: IDebugProgramEx2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2d3abc956d736f5c9273134b41c0fc9c2dc7db62
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65688942"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口使会话调试管理器 (SDM) 附加到程序并获取与程序关联的程序节点。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProgramEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 自定义端口提供程序在与 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口相同的对象上实现此接口，以便使 SDM 附加到某个程序，同时允许该端口供应商跟踪附加到该程序的所有会话。 自定义端口供应商可以在选择的情况下实现此接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 SDM 调用接口[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上的 QueryInterface `IDebugProgram2` 以获取此接口以跟踪已附加到程序的会话。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugProgramEx2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|将程序附加到会话。|  
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|获取与程序关联的程序节点。|  
  
## <a name="remarks"></a>备注  
 此接口在 SDM 和程序之间是私有的。  
  
## <a name="requirements"></a>要求  
 标头： Portpriv  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
