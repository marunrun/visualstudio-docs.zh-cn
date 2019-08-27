---
title: MODULE_FLAGS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- MODULE_FLAGS
helpviewer_keywords:
- MODULE_FLAGS enumeration
ms.assetid: 0e555b42-b846-4dbb-812e-8e3d11c85b2d
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ae51d604f455b12fd6933a54954b75a97aea4eb7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62547463"
---
# <a name="moduleflags"></a>MODULE_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

用于描述模块。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_MODULE_FLAGS {   
   MODULE_FLAG_NONE        = 0x0000,  
   MODULE_FLAG_SYSTEM      = 0x0001,  
   MODULE_FLAG_SYMBOLS     = 0x0002,  
   MODULE_FLAG_64BIT       = 0x0004,  
   MODULE_FLAG_OPTIMIZED   = 0x0008,  
   MODULE_FLAG_UNOPTIMIZED = 0x0010  
};  
typedef DWORD MODULE_FLAGS;  
```  
  
```csharp  
public enum enum_MODULE_FLAGS {   
   MODULE_FLAG_NONE        = 0x0000,  
   MODULE_FLAG_SYSTEM      = 0x0001,  
   MODULE_FLAG_SYMBOLS     = 0x0002,  
   MODULE_FLAG_64BIT       = 0x0004,  
   MODULE_FLAG_OPTIMIZED   = 0x0008,  
   MODULE_FLAG_UNOPTIMIZED = 0x0010  
};  
```  
  
## <a name="members"></a>成员  
 MODULE_FLAG_NONE  
 指定没有模块。  
  
 MODULE_FLAG_SYSTEM  
 指定系统模块。  
  
 MODULE_FLAG_SYMBOLS  
 指定符号的模块。  
  
 MODULE_FLAG_64BIT  
 指定的 64 位模块。  
  
 MODULE_FLAG_OPTIMIZED  
 指定该模块已进行了优化。 此状态反映在**模块**窗口。  
  
 MODULE_FLAG_UNOPTIMIZED  
 指定该模块未经过优化。 此状态反映在**模块**窗口。 这是默认状态。  
  
## <a name="remarks"></a>备注  
 用于`m_dwModuleFlags`的成员[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)结构。  
  
 可能的按位组合这些标志`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
