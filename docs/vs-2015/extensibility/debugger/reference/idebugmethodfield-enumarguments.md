---
title: IDebugMethodField::EnumArguments |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumArguments
helpviewer_keywords:
- IDebugMethodField::EnumArguments method
ms.assetid: 3ab55488-2437-4ff6-a9ae-78ea6d7b23a8
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5744e25f76676e70e25777596fb0d8eb3a580511
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205223"
---
# <a name="idebugmethodfieldenumarguments"></a>IDebugMethodField::EnumArguments
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建调用该方法所需的每个参数的类型的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumArguments(   
   IEnumDebugFields** ppParams  
);  
```  
  
```csharp  
int EnumArguments(  
   out IEnumDebugFields ppParams  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppParams`  
 [out]返回[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象，表示自变量类型的列表。 如果没有任何自变量，则返回 null 值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK 或如果没有任何自变量，则返回 S_FALSE。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 每个元素均[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象，表示每个参数的类型。 调用[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)方法来检索有关每个参数的类型的信息。  
  
 如果参数的名称需要与类型一起使用，然后调用[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)
