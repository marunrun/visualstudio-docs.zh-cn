---
title: BP_PASSCOUNT_STYLE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT_STYLE
helpviewer_keywords:
- BP_PASSCOUNT_STYLE structure
ms.assetid: 0a647047-e2d5-4724-a0b8-68108425ecad
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: deb4ce7c464e8518faff55957e1873ef1cd92c39
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153369"
---
# <a name="bp_passcount_style"></a>BP_PASSCOUNT_STYLE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定与导致断点激发的断点传递计数相关联的条件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_BP_PASSCOUNT_STYLE {   
   BP_PASSCOUNT_NONE             = 0x0000,  
   BP_PASSCOUNT_EQUAL            = 0x0001,  
   BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,  
   BP_PASSCOUNT_MOD              = 0x0003  
};  
typedef DWORD BP_PASSCOUNT_STYLE;  
```  
  
```csharp  
public enum enum_BP_PASSCOUNT_STYLE {   
   BP_PASSCOUNT_NONE             = 0x0000,  
   BP_PASSCOUNT_EQUAL            = 0x0001,  
   BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,  
   BP_PASSCOUNT_MOD              = 0x0003  
};  
```  
  
## <a name="members"></a>成员  
 BP_PASSCOUNT_NONE  
 指定没有断点传递计数样式。  
  
 BP_PASSCOUNT_EQUAL  
 将断点传递计数样式设置为相等。 命中断点的次数等于传递计数时，将激发断点。  
  
 BP_PASSCOUNT_EQUAL_OR_GREATER  
 将断点传递计数样式设置为等于或大于。 命中断点的次数等于或大于传递计数时，将激发断点。  
  
 BP_PASSCOUNT_MOD  
 指定模 pass 计数。 例如，如果传递计数为类型 `BP_PASSCOUNT_MOD` 并且传递计数值为4，则每次命中计数为4的倍数时都会触发断点。  
  
## <a name="remarks"></a>备注  
 用于作为 `stylePassCount` [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)和[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构的成员的[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构的成员。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
