---
title: IDebugBreakpointBoundEvent2::EnumBoundBreakpoints |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
helpviewer_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
ms.assetid: 1f588feb-522e-488d-be92-7bc19b9e3688
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bc3d38344dccf93f4b032357b2cdef88a0a4a242
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156122"
---
# <a name="idebugbreakpointboundevent2enumboundbreakpoints"></a>IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建已绑定到此事件的断点的枚举器。  
  
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
 [out]返回[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)此事件从绑定枚举所有断点的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`是否存在任何绑定的断点; 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 绑定断点的列表用于这些绑定到此事件，可能不是绑定从挂起断点的断点的完整列表。 若要获取所有绑定到挂起断点的断点的列表，请调用[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)方法以获取相关联[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)对象，然后调用[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)方法以获取[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)对象，其中包含有关挂起断点的所有绑定的断点。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于**CBreakpointSetDebugEventBase**对象，它公开[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)接口。  
  
```cpp#  
STDMETHODIMP CBreakpointSetDebugEventBase::EnumBoundBreakpoints(  
    IEnumDebugBoundBreakpoints2 **ppEnum)  
{  
    HRESULT hRes = E_FAIL;  
  
    if ( ppEnum )  
    {  
        if ( m_pEnumBound )  
        {  
            hRes = m_pEnumBound->Clone(ppEnum);  
  
            if ( EVAL(S_OK == hRes) )  
                (*ppEnum)->Reset();  
        }  
        else  
            hRes = E_FAIL;  
    }  
    else  
        hRes = E_INVALIDARG;  
  
    return ( hRes );  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)   
 [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)   
 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)   
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
