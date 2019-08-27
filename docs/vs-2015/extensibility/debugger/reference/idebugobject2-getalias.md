---
title: IDebugObject2::GetAlias |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject2::GetAlias
helpviewer_keywords:
- IDebugObject2::GetAlias method
ms.assetid: aa6824d5-c932-42ba-8713-950e7d1fb42f
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b05d416da41265f6727df843b1b686fcfe5107f7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194614"
---
# <a name="idebugobject2getalias"></a>IDebugObject2::GetAlias
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

如果有，获取与此对象相关联的别名。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetAlias(  
   IDebugAlias** ppAlias  
);  
```  
  
```csharp  
int GetAlias(  
   out IDebugAlias ppAlias  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppAlias`  
 [out]返回[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)对象，表示此对象的别名; 否则，返回 null 值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK;否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 通过调用创建一个对象的别名[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)   
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
