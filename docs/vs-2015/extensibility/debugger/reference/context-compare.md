---
title: CONTEXT_COMPARE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9cf283cf7239b5ed74e38ca534538a286a477c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179971"
---
# <a name="context_compare"></a>CONTEXT_COMPARE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定用于比较两个内存上下文的条件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_CONTEXT_COMPARE {   
   CONTEXT_EQUAL                 = 0x0001,  
   CONTEXT_LESS_THAN             = 0x0002,  
   CONTEXT_GREATER_THAN          = 0x0003,  
   CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,  
   CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,  
   CONTEXT_SAME_SCOPE            = 0x0006,  
   CONTEXT_SAME_FUNCTION         = 0x0007,  
   CONTEXT_SAME_MODULE           = 0x0008,  
   CONTEXT_SAME_PROCESS          = 0x0009  
};  
typedef DWORD CONTEXT_COMPARE;  
```  
  
```csharp  
public enum enum_CONTEXT_COMPARE {   
   CONTEXT_EQUAL                 = 0x0001,  
   CONTEXT_LESS_THAN             = 0x0002,  
   CONTEXT_GREATER_THAN          = 0x0003,  
   CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,  
   CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,  
   CONTEXT_SAME_SCOPE            = 0x0006,  
   CONTEXT_SAME_FUNCTION         = 0x0007,  
   CONTEXT_SAME_MODULE           = 0x0008,  
   CONTEXT_SAME_PROCESS          = 0x0009  
};  
```  
  
## <a name="members"></a>成员  
 CONTEXT_EQUAL  
 在列表中查找与目标内存上下文相等的第一个内存上下文。  
  
 CONTEXT_LESS_THAN  
 在列表中查找小于目标内存上下文的第一个内存上下文。  
  
 CONTEXT_GREATER_THAN  
 在列表中查找大于目标内存上下文的第一个内存上下文。  
  
 CONTEXT_LESS_THAN_OR_EQUAL  
 在列表中查找小于或等于目标内存上下文的第一个内存上下文。  
  
 CONTEXT_GREATER_THAN_OR_EQUAL  
 在列表中查找大于或等于目标内存上下文的第一个内存上下文。  
  
 CONTEXT_SAME_SCOPE  
 在列表中查找与目标内存上下文相同的范围中的第一个内存上下文。  
  
 CONTEXT_SAME_FUNCTION  
 在列表中查找第一个与目标内存范围处于相同函数的内存上下文。  
  
 CONTEXT_SAME_MODULE  
 在与目标内存上下文相同的模块中查找列表中的第一个内存上下文。  
  
 CONTEXT_SAME_PROCESS  
 在列表中查找与目标内存上下文相同的进程中的第一个内存上下文。  
  
## <a name="remarks"></a>备注  
 作为参数传递给 [Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md) 方法。  
  
 这些值用于在满足指定比较条件的列表中查找第一个内存上下文。 将为内存上下文提供要与方法进行比较的内存上下文的列表 `IDebugMemoryContext2::Compare` 。 然后返回该列表中比较运算符所属的第一个内存上下文 `true` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [比较](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)
