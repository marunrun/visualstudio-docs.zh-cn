---
title: IDebugMethodField::EnumLocals |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2306bbf0c44a883c584346c3dbb3dd70e9b39175
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162605"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建所选的方法的局部变量的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumLocals(   
   IDebugAddress*     pAddress,  
   IEnumDebugFields** ppLocals  
);  
```  
  
```csharp  
int EnumLocals(  
   IDebugAddress        pAddress,   
   out IEnumDebugFields ppLocals  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pAddress`  
 [in][IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象，表示选择的上下文或从其获取局部变量的作用域的调试地址。  
  
 `ppLocals`  
 [out]返回[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象，表示局部变量的列表; 否则，返回 null 值，如果不有任何局部变量。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK 或如果没有局部变量，则返回 S_FALSE。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 将枚举中仅包含给定的调试地址块中定义的变量。 如果需要包括任何编译器生成的局部变量的所有局部变量，调用[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)方法。  
  
 一种方法可以包含多个作用域的上下文或块。 例如，以下精心设计的方法包含三个作用域、 两个内部块和方法主体本身。  
  
```csharp  
public void func(int index)  
{  
    // Method body scope  
    int a = 0;  
    if (index == 1)  
    {  
        // Inner scope 1  
        int temp1 = a;  
    }  
    else  
    {  
        // Inner scope 2  
        int temp2 = a;  
    }  
}  
```  
  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)对象表示`func`方法本身。 调用`EnumLocals`方法替换[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)设置为`Inner Scope 1`地址返回一个枚举，其中包含`temp1`变量，例如。  
  
## <a name="see-also"></a>请参阅  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)   
 [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
