---
title: IDebugBoundBreakpoint2::Enable |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::Enable
helpviewer_keywords:
- Enable method
- IDebugBoundBreakpoint2::Enable method
ms.assetid: 1b4e3f73-c94d-4aa3-9aa8-0d8cb8a6c5ca
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c650ff26b1ce7358312ef90bc737f2f911b0a52f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156273"
---
# <a name="idebugboundbreakpoint2enable"></a>IDebugBoundBreakpoint2::Enable
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

启用或禁用断点。  
  
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
 [in]设置为非零值 (`TRUE`) 若要启用或为零 (`FALSE`) 若要禁用的断点。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回`E_BP_DELETED`如果绑定的断点对象的状态设置为`BPS_DELETED`(属于[BP_STATE](../../../extensibility/debugger/reference/bp-state.md)枚举)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于简单`CBoundBreakpoint`公开的对象[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)接口。  
  
```  
HRESULT CBoundBreakpoint::Enable(BOOL fEnable)    
{    
   HRESULT hr;    
  
   // Verify that the bound breakpoint has not been deleted. If deleted,   
   // then return hr = E_BP_DELETED.    
   if (m_state != BPS_DELETED)    
   {    
      // Check the state of the bound breakpoint. If the breakpoint is  
      // supposed to be, but has not already been, enabled, then have the  
      // interpreter set the breakpoint.    
      if (fEnable && m_state != BPS_ENABLED)    
      {    
         hr = m_pInterp->SetBreakpoint(m_sbstrDoc, this);    
         if (hr == S_OK)    
         {    
            // Change the state of the breakpoint to BPS_ENABLED.    
            m_state = BPS_ENABLED;    
         }    
      }    
      // Check the state of the bound breakpoint. If the breakpoint is   
      // supposed to be, but has not already been, disabled, then have the   
      // interpreter remove the breakpoint.    
      else if (!fEnable && m_state != BPS_DISABLED)    
      {    
         hr = m_pInterp->RemoveBreakpoint(m_sbstrDoc, this);    
         if (hr == S_OK)    
         {    
            // Change the state of the breakpoint to BPS_DISABLED.    
            m_state = BPS_DISABLED;    
         }    
      }    
      else    
      {    
         hr = S_FALSE;    
      }    
   }    
   else    
   {    
      hr = E_BP_DELETED;    
   }    
  
   return hr;    
}    
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)   
 [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
