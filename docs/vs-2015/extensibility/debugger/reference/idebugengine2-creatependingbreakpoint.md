---
title: IDebugEngine2：： CreatePendingBreakpoint |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 84c36d08c7ad907006eb9f41d2f6e2c9cd77e7bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196033"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

 (DE) ，在调试引擎中创建挂起断点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT CreatePendingBreakpoint(   
   IDebugBreakpointRequest2*  pBPRequest,  
   IDebugPendingBreakpoint2** ppPendingBP  
);  
```  
  
```csharp  
int CreatePendingBreakpoint(   
   IDebugBreakpointRequest2     pBPRequest,  
   out IDebugPendingBreakpoint2 ppPendingBP  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pBPRequest`  
 中描述要创建的挂起断点的 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) 对象。  
  
 `ppPendingBP`  
 弄返回一个 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 对象，该对象表示挂起的断点。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 如果参数不 `E_FAIL` `pBPRequest` 匹配（如果 `pBPRequest` 参数无效或不完整）所支持的任何语言，则通常返回。  
  
## <a name="remarks"></a>备注  
 挂起断点实质上是将断点绑定到代码所需的所有信息的集合。 在调用 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) 方法之前，从此方法返回的挂起断点不会绑定到代码。  
  
 对于用户设置的每个挂起的断点，会话调试管理器 (SDM) 在每个附加的 DE 中调用此方法。 这是为了验证断点对于在该 DE 中运行的程序是否有效。  
  
 当用户在代码行上设置断点时，可以自由地将断点绑定到文档中对应于此代码的最接近的行。 这样一来，用户就可以在多行语句的第一行上设置断点，但将其绑定到在调试信息) 中所有代码都特性 (的最后一行。  
  
## <a name="example"></a>示例  
 下面的示例演示如何为简单对象实现此方法 `CProgram` 。 在的实现 `IDebugEngine2::CreatePendingBreakpoint` 中，可能会在每个程序中将对该方法实现的所有调用转发给。  
  
```  
HRESULT CProgram::CreatePendingBreakpoint(IDebugBreakpointRequest2* pBPRequest, IDebugPendingBreakpoint2** ppPendingBP)     
{    
  
   // Create and initialize the CPendingBreakpoint object.  
   CComObject<CPendingBreakpoint> *pPending;    
   CComObject<CPendingBreakpoint>::CreateInstance(&pPending);    
   pPending->Initialize(pBPRequest, m_pInterp, m_pCallback, m_pEngine);    
   return pPending->QueryInterface(ppPendingBP);    
}    
```  
  
## <a name="see-also"></a>另请参阅  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)   
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)   
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
