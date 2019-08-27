---
title: IDebugExceptionEvent2::GetException |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetException
helpviewer_keywords:
- IDebugExceptionEvent2::GetException
ms.assetid: 7c98f41d-322b-4e72-a514-cbd4823eb70d
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a0e19dc924101fcceb93948272fc1e83353e2815
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163800"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取触发此事件的异常的详细的说明。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetException(   
   EXCEPTION_INFO* pExceptionInfo  
);  
```  
  
```csharp  
int GetException(   
   EXCEPTION_INFO[] pExceptionInfo  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pExceptionInfo`  
 [in、 out][EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)使用异常的说明填充的结构。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 [C++仅]调用方负责释放中的任何字符串[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)结构，以及释放[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)结构中的对象。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)   
 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
