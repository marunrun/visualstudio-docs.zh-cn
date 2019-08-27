---
title: IDebugEvent2::GetAttributes |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEvent2::GetAttributes
helpviewer_keywords:
- IDebugEvent2::GetAttributes
ms.assetid: 2ac5b5fb-da17-43f7-811a-313f677e60d7
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8396d633e682eb9c78aef5b1241e7f9fc635a325
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68144381"
---
# <a name="idebugevent2getattributes"></a>IDebugEvent2::GetAttributes
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取此调试事件的特性。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetAttribute(   
   DWORD* pdwAttrib  
);  
```  
  
```csharp  
int GetAttribute(   
   out uint pdwAttrib  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pdwAttrib`  
 [out]中的标志的组合[EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)枚举。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口是普遍适用于所有事件。 此方法描述类型的事件;例如，是同步还是异步事件并将它停止事件。  
  
## <a name="see-also"></a>请参阅  
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
