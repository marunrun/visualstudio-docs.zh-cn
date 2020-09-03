---
title: IDebugEngine3：： SetAllExceptions |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetAllExceptions
helpviewer_keywords:
- IDebugEngine3::SetAllExceptions
ms.assetid: 8f03a6ac-a854-42f7-933c-a2df1b351975
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 48abbfb47e346ad9acbfac7b92642e6638f67df3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195901"
---
# <a name="idebugengine3setallexceptions"></a>IDebugEngine3::SetAllExceptions
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法设置所有未处理异常的状态。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT SetAllExceptions(  
   EXCEPTION_STATE dwState  
);  
```  
  
```csharp  
int SetAllExceptions(  
   enum_EXCEPTION_STATE dwState  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwState`  
 中 [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md) 值之一。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)   
 [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)
