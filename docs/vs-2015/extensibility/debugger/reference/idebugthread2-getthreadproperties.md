---
title: IDebugThread2::GetThreadProperties |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::GetThreadProperties
helpviewer_keywords:
- IDebugThread2::GetThreadProperties
ms.assetid: 304403fd-f4f8-4096-ac2c-bd3b59663aad
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dd32c32d2ccdb041ea34ce8d9d7ca72f2035db94
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152999"
---
# <a name="idebugthread2getthreadproperties"></a>IDebugThread2::GetThreadProperties
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取描述此线程的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetThreadProperties (   
   THREADPROPERTY_FIELDS dwFields,  
   THREADPROPERTIES*     ptp  
);  
```  
  
```csharp  
int GetThreadProperties (   
   enum_THREADPROPERTY_FIELDS dwFields,  
   THREADPROPERTIES[]         ptp  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwFields`  
 [in]中的标志的组合[THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)枚举，它确定的哪些字段`ptp`要填充的。  
  
 `ptp`  
 [in、 out]一个[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)填充线程的属性的结构。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 通常，此方法返回的信息显示在**线程**调试窗口。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于简单`CProgram`对象，它实现[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)接口。  
  
```cpp#  
HRESULT CProgram::GetThreadProperties(THREADPROPERTY_FIELDS dwFields,  
                                      THREADPROPERTIES *ptp)  
{  
    HRESULT hr = E_FAIL;    
  
    // Check for valid argument.    
   if (ptp)    
    {    
      // Create an array of buffers at ptp the size of the  
      // THREADPROPERTIES structure and set all of the  
      // buffers at ptp to 0.    
      memset(ptp, 0, sizeof (THREADPROPERTIES));    
  
      // Check if there is a valid THREADPROPERTY_FIELDS and the TPF_ID flag is set.    
      if (dwFields & TPF_ID)    
      {    
         // Check for successful assignment of the current thread ID to  
         //  the dwThreadId of the passed THREADPROPERTIES.    
         if (GetThreadId(&(ptp->dwThreadId)) == S_OK)    
         {    
            // Set the TPF_ID flag in the THREADPROPERTY_FIELDS enumerator    
            // of the passed THREADPROPERTIES.    
            ptp->dwFields |= TPF_ID;    
         }    
      }    
  
      hr = S_OK;    
    }    
    else    
        hr = E_INVALIDARG;    
  
    return hr;    
}    
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)   
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
