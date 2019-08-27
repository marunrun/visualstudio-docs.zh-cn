---
title: IDebugPendingBreakpoint2::Enable |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Enable
helpviewer_keywords:
- IDebugPendingBreakpoint2::Enable method
- Enable method
ms.assetid: 09e32d05-464b-40a6-a41d-76f2759cf2cd
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f5dc3c1e37a817c1c962d05745db33422008c550
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194495"
---
# <a name="idebugpendingbreakpoint2enable"></a>IDebugPendingBreakpoint2::Enable
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

切换挂起断点的启用的状态。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Enable(   
   BOOL fEnable  
);  
```  
  
```csharp  
int Enable(   
   int fEnable  
);  
```  
  
#### <a name="parameters"></a>参数  
 `fEnable`  
 [in]设置为非零值 (`TRUE`) 以启用挂起断点，或为零 (`FALSE`) 若要禁用。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回`E_BP_DELETED`如果断点已被删除。  
  
## <a name="remarks"></a>备注  
 当启用或禁用挂起断点，从该绑定的所有断点都设置为相同的状态。  
  
 可能有必要，请根据多次调用此方法，即使已启用或禁用断点。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于简单`CPendingBreakpoint`公开的对象[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口。  
  
```cpp#  
HRESULT CPendingBreakpoint::Enable(BOOL fEnable)    
{    
   HRESULT hr;    
  
   // Verify that the pending breakpoint has not been deleted. If deleted,   
   // then return hr = E_BP_DELETED.    
   if (m_state.state != PBPS_DELETED)    
   {    
      // If the bound breakpoint member variable is valid, then enable or   
      // disable the bound breakpoint.    
      if (m_pBoundBP)    
      {    
         m_pBoundBP->Enable(fEnable);    
      }    
      // Set the PENDING_BP_STATE in the PENDING_BP_STATE_INFO structure   
      // to enabled or disabled depending on the passed BOOL condition.    
      m_state.state = fEnable ? PBPS_ENABLED : PBPS_DISABLED;    
      hr = S_OK;    
  
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
