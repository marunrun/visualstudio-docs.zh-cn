---
title: BP_PASSCOUNT_STYLE | Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153369"
---
# <a name="bppasscountstyle"></a>BP_PASSCOUNT_STYLE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定将导致触发该断点的断点传递计数与相关联的条件。  
  
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
 不指定任何断点传递计数样式。  
  
 BP_PASSCOUNT_EQUAL  
 设置为等于断点传递计数样式。 当命中断点次数等于传递计数时，将触发断点。  
  
 BP_PASSCOUNT_EQUAL_OR_GREATER  
 将断点传递计数样式设置为相等或更高版本。 当命中断点次数等于或大于传递计数时，将触发断点。  
  
 BP_PASSCOUNT_MOD  
 指定取模传递计数。 例如，如果类型是传递计数`BP_PASSCOUNT_MOD`和传递计数值为 4，断点将触发每次命中的计数是 4 的倍数。  
  
## <a name="remarks"></a>备注  
 用于`stylePassCount`的成员[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构，它又是的成员[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)并[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
