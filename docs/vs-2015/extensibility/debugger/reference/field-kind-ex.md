---
title: FIELD_KIND_EX | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- FIELD_KIND_EX enumeration
ms.assetid: 922c3208-1e94-485f-b70a-3bc96affeff8
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7e6384ea963fe1da145cacc0be46b5989f7bc610
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198752"
---
# <a name="fieldkindex"></a>FIELD_KIND_EX
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举其他类型的字段的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象可包含。 此枚举扩展[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)枚举。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_FIELD_KIND_EX  
{  
   FIELD_KIND_EX_NONE = 0,  
   FIELD_TYPE_EX_METHODVAR = 0x1,  
   FIELD_TYPE_EX_CLASSVAR = 0x2  
} ;  
typedef DWORD FIELD_KIND_EX;  
```  
  
```csharp  
public enum enum_FIELD_KIND_EX  
{  
   FIELD_KIND_EX_NONE = 0,  
   FIELD_TYPE_EX_METHODVAR = 0x1,  
   FIELD_TYPE_EX_CLASSVAR = 0x2  
};  
```  
  
## <a name="members"></a>成员  
 FIELD_KIND_EX_NONE  
 字段不包含扩展的类型。  
  
 FIELD_TYPE_EX_METHODVAR  
 字段包含一个方法的变量。  
  
 FIELD_TYPE_EX_CLASSVAR  
 字段包含一个类变量。  
  
## <a name="requirements"></a>要求  
 标头：Sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)
