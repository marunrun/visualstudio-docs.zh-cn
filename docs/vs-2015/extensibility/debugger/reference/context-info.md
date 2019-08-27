---
title: CONTEXT_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CONTEXT_INFO
helpviewer_keywords:
- CONTEXT_INFO structure
ms.assetid: 6b513f4e-e7b0-4969-adf0-2205ccc1e09b
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4e8c1b438cd2fa2721e81f055695e5836c26d12
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179945"
---
# <a name="contextinfo"></a>CONTEXT_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此结构描述内存上下文或代码上下文。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _tagCONTEXT_INFO {   
   CONTEXT_INFO_FIELDS dwFields;  
   BSTR                bstrModuleUrl;  
   BSTR                bstrFunction;  
   TEXT_POSITION       posFunctionOffset;  
   BSTR                bstrAddress;  
   BSTR                bstrAddressOffset;  
   BSTR                bstrAddressAbsolute;  
} CONTEXT_INFO;  
```  
  
```csharp  
public struct CONTEXT_INFO {  
   public uint          dwFields;  
   public string        bstrModuleUrl;  
   public string        bstrFunction;  
   public TEXT_POSITION posFunctionOffset;  
   public string        bstrAddress;  
   public string        bstrAddressOffset;  
   public string        bstrAddressAbsolute;  
};  
```  
  
## <a name="members"></a>成员  
 dwFields  
 从他的标志的组合[CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)枚举，用于指定哪些字段填完<strong>。</strong>  
  
 bstrModuleUrl  
 上下文的位置的模块的名称。  
  
 bstrFunction  
 函数名称上下文所在的位置。  
  
 posFunctionOffset  
 一个[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构，它标识与代码上下文关联的函数的行和列偏移量。  
  
 bstrAddress  
 给定的上下文的位置的代码中的地址。  
  
 bstrAddressOffset  
 在代码中给定的上下文的位置的地址的偏移量。  
  
 bstrAddressAbsolute  
 给定的上下文的位置的内存中的绝对地址。  
  
## <a name="remarks"></a>备注  
 此结构从调用返回[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)方法。  
  
 此结构的典型用法是支持**内存**调试窗口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)   
 [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
