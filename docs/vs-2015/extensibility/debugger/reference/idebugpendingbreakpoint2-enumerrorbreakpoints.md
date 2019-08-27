---
title: IDebugPendingBreakpoint2::EnumErrorBreakpoints |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::EnumErrorBreakpoints
helpviewer_keywords:
- IDebugPendingBreakpoint2::EnumErrorBreakpoints method
- EnumErrorBreakpoints method
ms.assetid: 2f9a9720-c1ac-4430-8f28-200d85360452
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f9cac8b19e6281b8993e84d13ae60138ddaeac89
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201083"
---
# <a name="idebugpendingbreakpoint2enumerrorbreakpoints"></a>IDebugPendingBreakpoint2::EnumErrorBreakpoints
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取来自此挂起断点的所有错误断点的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumErrorBreakpoints(   
   BP_ERROR_TYPE                 bpErrorType,  
   IEnumDebugErrorBreakpoints2** ppEnum  
);  
```  
  
```csharp  
int EnumErrorBreakpoints(   
   enum_BP_ERROR_TYPE              bpErrorType,  
   out IEnumDebugErrorBreakpoints2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `bpErrorType`  
 [in]中值的组合[BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)选择要枚举的错误的类型的枚举。  
  
 `ppEnum`  
 [out]返回[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)对象，其中包含一系列[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回`E_BP_DELETED`如果断点已被删除。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于简单`CPendingBreakpoint`公开的对象[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)接口。  
  
```cpp#  
HRESULT CPendingBreakpoint::EnumErrorBreakpoints(  
   BP_ERROR_TYPE bpErrorType,  
   IEnumDebugErrorBreakpoints2** ppEnum)    
{    
   HRESULT hr;    
  
   // Verify that the passed IEnumDebugErrorBreakpoints2 interface pointer   
   // is valid.    
   if (ppEnum)    
   {    
      // Verify that the pending breakpoint has not been deleted. If   
      // deleted, then return hr = E_BP_DELETED.    
      if (m_state.state != PBPS_DELETED)    
      {    
         // Verify that this error is not a warning.    
         // All errors supported by this DE are errors, not warnings.    
         if (IsFlagSet(bpErrorType, BPET_TYPE_ERROR) && m_pErrorBP)    
         {    
            // Get the error breakpoint.    
            CComPtr<IDebugErrorBreakpoint2> spErrorBP;    
            hr = m_pErrorBP->QueryInterface(&spErrorBP);    
            assert(hr == S_OK);    
            if (hr == S_OK)    
            {    
               // Create the error breakpoint enumerator.    
               CComObject<CEnumDebugErrorBreakpoints>* pErrorEnum;    
               hr = CComObject<CEnumDebugErrorBreakpoints>::CreateInstance(&pErrorEnum);    
               assert(hr == S_OK);    
               if (hr == S_OK)    
               {    
                  // Initialize the enumerator of error breakpoints with   
                  // the IDebugErrorBreakpoint2 information.      
                  IDebugErrorBreakpoint2* rgpErrorBP[] = { spErrorBP.p };    
                  hr = pErrorEnum->Init(rgpErrorBP, &(rgpErrorBP[1]), NULL, AtlFlagCopy);    
                  if (hr == S_OK)    
                  {    
                     // Verify that the passed IEnumDebugErrorBreakpoints2     
                     // interface can be queried by the created   
                     // CEnumDebugErrorBreakpoints object.    
                     hr = pErrorEnum->QueryInterface(ppEnum);    
                     assert(hr == S_OK);    
                  }    
  
                  // Otherwise, delete the CEnumDebugErrorBreakpoints   
                  // object.    
                  if (FAILED(hr))    
                  {    
                     delete pErrorEnum;    
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
  
## <a name="see-also"></a>请参阅  
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)   
 [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)   
 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
