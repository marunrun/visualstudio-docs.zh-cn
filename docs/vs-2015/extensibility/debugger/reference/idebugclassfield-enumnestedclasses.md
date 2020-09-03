---
title: IDebugClassField：： EnumNestedClasses |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedClasses
helpviewer_keywords:
- IDebugClassField::EnumNestedClasses method
ms.assetid: 2ba5ef0c-395e-4006-9e3c-9b06e1d711d0
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7745eea3f5b3264016a25defd696a9b85f2e9fb4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191071"
---
# <a name="idebugclassfieldenumnestedclasses"></a>IDebugClassField::EnumNestedClasses
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建嵌套在此类中的类的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumNestedClasses(   
   IEnumDebugFields** ppEnum  
);  
```  
  
```csharp  
int EnumNestedClasses(  
   out IEnumDebugFields ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppEnum`  
 弄返回一个 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象，该对象表示嵌套类的列表。 如果没有嵌套类，则返回 null 值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK 或返回 S_FALSE （如果没有嵌套类）。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 枚举的每个元素都是一个描述嵌套类的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。  
  
 嵌套类是在另一个类中定义的类。 例如：  
  
```  
class RootClass {  
   class NestedClass { }  
};  
```  
  
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)枚举将包含一个表示类的对象 `NestedClass` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
