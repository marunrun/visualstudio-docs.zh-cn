---
title: IDebugEngine2::ContinueFromSynchronousEvent |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine2::ContinueFromSynchronousEvent
helpviewer_keywords:
- IDebugEngine2::ContinueFromSynchronousEvent
ms.assetid: 9a57dfcd-df8e-4be5-b1fe-bd853e3c6bb2
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 75c359f8d7f7c0c5e9d335de296fe252b30d1c3d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198464"
---
# <a name="idebugengine2continuefromsynchronousevent"></a>IDebugEngine2::ContinueFromSynchronousEvent
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

由会话调试管理器 (SDM) 以指示同步调试事件，以前由调试引擎 (DE) 发送到 SDM，已接收并处理调用。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT ContinueFromSynchronousEvent(   
   IDebugEvent2* pEvent  
);  
```  
  
```csharp  
HRESULT ContinueFromSynchronousEvent(   
   IDebugEvent2 pEvent  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pEvent`  
 [in][IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)对象，表示从其调试器现在应继续先前发送的同步事件。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 DE 必须验证它是否表示的事件的源`pEvent`参数。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于简单`CEngine`对象，它实现[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口。  
  
```cpp#  
HRESULT CEngine::ContinueFromSynchronousEvent(IDebugEvent2* pEvent)  
{  
   HRESULT hr;  
  
   // Create a pointer to a unique event interface defined for batch file  
   // breaks.    
   IAmABatchFileEvent *pBatEvent;  
   // Check for successful query for the unique batch file event  
   // interface.  
   if (SUCCEEDED(pEvent->QueryInterface(IID_IAmABatchFileEvent,  
                                       (void **)&pBatEvent)))  
   {  
      // Release the result of the QI.  
      pBatEvent->Release();  
      // Check thread message for notification to continue.  
      if (PostThreadMessage(GetCurrentThreadId(),  
                            WM_CONTINUE_SYNC_EVENT,  
                            0,  
                            0))  
      {    
         hr = S_OK;  
      }  
      else  
      {  
         hr = HRESULT_FROM_WIN32(GetLastError());  
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
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
