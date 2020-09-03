---
title: IDebugPendingBreakpoint2：： EnumBoundBreakpoints |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::EnumBoundBreakpoints
helpviewer_keywords:
- EnumBoundBreakpoints method
- IDebugPendingBreakpoint2::EnumBoundBreakpoints method
ms.assetid: 179c7c54-8446-462d-b099-e0f9cf06dc52
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ccbd3e3d54382550201771ecc8f9fbad3bca849d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194474"
---
# <a name="idebugpendingbreakpoint2enumboundbreakpoints"></a>IDebugPendingBreakpoint2::EnumBoundBreakpoints
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举从此挂起断点绑定的所有断点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumBoundBreakpoints(   
   IEnumDebugBoundBreakpoints2** ppEnum  
);  
```  
  
```csharp  
int EnumBoundBreakpoints(   
   out IEnumDebugBoundBreakpoints2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppEnum`  
 弄返回一个 [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) 对象，该对象枚举绑定的断点。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_BP_DELETED`如果已删除断点，则返回。  
  
## <a name="example"></a>示例  
 下面的示例演示如何为 `CPendingBreakpoint` 公开 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 接口的简单对象实现此方法。  
  
```cpp#  
HRESULT CPendingBreakpoint::EnumBoundBreakpoints(IEnumDebugBoundBreakpoints2** ppEnum)    
{    
   HRESULT hr;    
  
   // Verify that the passed IEnumDebugBoundBreakpoints2 interface pointer   
   // is valid.    
   if (ppEnum)    
   {    
      *ppEnum = NULL;  
  
      // Verify that the pending breakpoint has not been deleted. If   
      // deleted, then return hr = E_BP_DELETED.    
      if (m_state.state != PBPS_DELETED)    
      {    
         // If the bound breakpoint member variable is valid.  
         if (m_pBoundBP)    
         {    
            // Get the bound breakpoint.    
            CComPtr<IDebugBoundBreakpoint2> spBoundBP;    
            hr = m_pBoundBP->QueryInterface(&spBoundBP);    
            assert(hr == S_OK);    
            if (hr == S_OK)    
            {    
               // Create the bound breakpoint enumerator.    
               CComObject<CEnumDebugBoundBreakpoints>* pBoundEnum;    
               hr = CComObject<CEnumDebugBoundBreakpoints>::CreateInstance(&pBoundEnum);    
               assert(hr == S_OK);    
               if (hr == S_OK)    
               {    
                  // Initialize the enumerator of bound breakpoints with   
                  // the IDebugBoundBreakpoint2 information.      
                  IDebugBoundBreakpoint2* rgBoundBP[] = { spBoundBP.p };    
                  hr = pBoundEnum->Init(rgBoundBP, &(rgBoundBP[1]), NULL, AtlFlagCopy);    
                  if (hr == S_OK)    
                  {    
                     // Verify that the passed IEnumDebugBoundBreakpoints2     
                     // interface can be queried by the created  
                     // CEnumDebugBoundBreakpoints object.    
                     hr = pBoundEnum->QueryInterface(ppEnum);    
                     assert(hr == S_OK);    
                  }    
  
                  // Otherwise, delete the CEnumDebugBoundBreakpoints object.    
                  if (FAILED(hr))    
                  {    
                     delete pBoundEnum;    
                  }    
               }    
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
   }    
   else    
   {    
      hr = E_INVALIDARG;    
   }    
  
   return hr;    
}    
```  
  
## <a name="see-also"></a>另请参阅  
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)
