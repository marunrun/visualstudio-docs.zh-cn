---
title: BPRESI_FIELDS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BPRESI_FIELDS
helpviewer_keywords:
- BPRESI_FIELDS enumeration
ms.assetid: 99f17b1e-3e67-4f85-89d6-5c6cf45c8008
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 52a4b9719b03c353dd3933c16b6f494f19f9c6ad
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153204"
---
# <a name="bpresifields"></a>BPRESI_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索有关断点的成功的解决方法的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_BPRESI_FIELDS {   
   BPRESI_BPRESLOCATION = 0x0001,  
   BPRESI_PROGRAM       = 0x0002,  
   BPRESI_THREAD        = 0x0004,  
   BPRESI_ALLFIELDS     = 0xffffffff  
};  
typedef DWORD BPRESI_FIELDS;  
```  
  
```csharp  
public enum enum_BPRESI_FIELDS {   
   BPRESI_BPRESLOCATION = 0x0001,  
   BPRESI_PROGRAM       = 0x0002,  
   BPRESI_THREAD        = 0x0004,  
   BPRESI_ALLFIELDS     = 0xffffffff  
};  
```  
  
## <a name="members"></a>成员  
 BPRESI_BPRESLOCATION  
 初始化/用`bpResLocation`（断点解析位置） 的字段[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)结构。  
  
 BPRESI_PROGRAM  
 初始化/用`pProgram`字段的`BP_RESOLUTION_INFO`结构。  
  
 BPRESI_THREAD  
 初始化/用`pThread`字段的`BP_RESOLUTION_INFO`结构。  
  
 BPRESI_ALLFIELDS  
 指定的所有字段。  
  
## <a name="remarks"></a>备注  
 传递给[GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)方法，以指示的哪些字段[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)结构是进行初始化。  
  
 这些标志还用于指示哪些字段的`BP_RESOLUTION_INFO`结构已使用且有效时返回该结构。  
  
 可能的按位组合这些值`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)   
 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
