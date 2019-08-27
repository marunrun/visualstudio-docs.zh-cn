---
title: BPERESI_FIELDS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BPERESI_FIELDS
helpviewer_keywords:
- BPERESI_FIELDS enumeration
ms.assetid: dd7dd89c-1043-46a1-a929-099cc039c344
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b1b5cba13e439c69b3502b00c6ae159b6af28178
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153237"
---
# <a name="bperesifields"></a>BPERESI_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索有关失败的解决方法的断点的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_BPERESI_FIELDS {   
   PERESI_BPRESLOCATION = 0x0001,  
   BPERESI_PROGRAM      = 0x0002,  
   BPERESI_THREAD       = 0x0004,  
   BPERESI_MESSAGE      = 0x0008,  
   BPERESI_TYPE         = 0x0010,  
   BPERESI_ALLFIELDS    = 0xffffffff  
};  
typedef DWORD BPERESI_FIELDS;  
```  
  
```csharp  
public enum enum_BPERESI_FIELDS {   
   PERESI_BPRESLOCATION = 0x0001,  
   BPERESI_PROGRAM      = 0x0002,  
   BPERESI_THREAD       = 0x0004,  
   BPERESI_MESSAGE      = 0x0008,  
   BPERESI_TYPE         = 0x0010,  
   BPERESI_ALLFIELDS    = 0xffffffff  
};  
```  
  
## <a name="members"></a>成员  
 PERESI_BPRESLOCATION  
 初始化/用`bpResLocation`（断点解析位置） 的字段[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)结构。  
  
 BPERESI_PROGRAM  
 初始化/用`pProgram`字段的`BP_ERROR_RESOLUTION_INFO`结构。  
  
 BPERESI_THREAD  
 初始化/用`pThread`字段的`BP_ERROR_RESOLUTION_INFO`结构。  
  
 BPERESI_MESSAGE  
 初始化/用`bstrMessage`字段的`BP_ERROR_RESOLUTION_INFO`结构。  
  
 BPERESI_TYPE  
 初始化/用`dwType`（断点类型） 字段的`BP_ERROR_RESOLUTION_INFO`结构。  
  
 BPERESI_ALLFIELDS  
 初始化/使用的所有字段`BP_ERROR_RESOLUTION_INFO`结构。  
  
## <a name="remarks"></a>备注  
 作为参数传递给[GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)方法，以指示的哪些字段[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)结构是进行初始化。  
  
 这些值还用于指示中的哪些字段`BP_ERROR_RESOLUTION_INFO`结构已使用且有效时返回该结构。  
  
 可能的按位组合这些值`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)   
 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
