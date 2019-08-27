---
title: IDebugPendingBreakpoint2::Delete | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Delete
helpviewer_keywords:
- IDebugPendingBreakpoint2::Delete method
- Delete method
ms.assetid: 4cb5ed81-6f0c-41ce-a770-5adb6b4bf5d9
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c70be92992cb8ef9e6664c29e838098efc7aed76
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194504"
---
# <a name="idebugpendingbreakpoint2delete"></a>IDebugPendingBreakpoint2::Delete
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

删除此挂起断点和从该绑定的所有断点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Delete(   
   void   
);  
```  
  
```csharp  
int Delete();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回`E_BP_DELETED`如果断点已被删除。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于简单`CPendingBreakpoint`对象，它实现[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口。  
  
```cpp#  
HRESULT CPendingBreakpoint::Delete(void)    
{    
   HRESULT hr;    
  
   // Verify that the pending breakpoint has not been deleted. If deleted,    
   // then return hr = E_BP_DELETED.    
   if (m_state.state != PBPS_DELETED)    
   {    
      // If the pending breakpoint has bound and has an associated bound   
      // breakpoint, delete and release the bound breakpoint and set the   
      // pointer to NULL.    
      if (m_pBoundBP)    
      {    
         m_pBoundBP->Delete();    
         m_pBoundBP->Release();    
         m_pBoundBP = NULL;    
      }    
      // If the pending breakpoint did not bind and has an associated   
      // error breakpoint, release the error breakpoint and set the   
      // pointer to NULL.   
      if (m_pErrorBP)    
      {    
         m_pErrorBP->Release();    
         m_pErrorBP = NULL;    
      }    
  
      // Set the PENDING_BP_STATE in the PENDING_BP_STATE_INFO structure   
      // to deleted.     
      m_state.state = PBPS_DELETED;    
   }    
   else    
   {    
      hr = E_BP_DELETED;    
   }    
  
   return hr;    
}    
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
