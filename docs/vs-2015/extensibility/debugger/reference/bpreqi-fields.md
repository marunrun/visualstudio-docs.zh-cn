---
title: BPREQI_FIELDS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BPREQI_FIELDS
helpviewer_keywords:
- BPREQI_FIELDS enumeration
ms.assetid: 679e771e-4a79-484e-af37-f962ef4aa245
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a8ad9e4b6d83ebc05c78a8b84c0c06e00d7563bc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153231"
---
# <a name="bpreqi_fields"></a>BPREQI_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要检索的有关断点请求的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
enum enum_BPREQI_FIELDS {   
   BPREQI_BPLOCATION   = 0x0001,  
   BPREQI_LANGUAGE     = 0x0002,  
   BPREQI_PROGRAM      = 0x0004,  
   BPREQI_PROGRAMNAME  = 0x0008,  
   BPREQI_THREAD       = 0x0010,  
   BPREQI_THREADNAME   = 0x0020,  
   BPREQI_PASSCOUNT    = 0x0040,  
   BPREQI_CONDITION    = 0x0080,  
   BPREQI_FLAGS        = 0x0100,  
   BPREQI_ALLOLDFIELDS = 0x01ff  
   BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only  
   BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only  
   BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only  
   BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only  
};  
typedef DWORD BPREQI_FIELDS;  
```  
  
```csharp  
public enum enum_BPREQI_FIELDS {   
   BPREQI_BPLOCATION   = 0x0001,  
   BPREQI_LANGUAGE     = 0x0002,  
   BPREQI_PROGRAM      = 0x0004,  
   BPREQI_PROGRAMNAME  = 0x0008,  
   BPREQI_THREAD       = 0x0010,  
   BPREQI_THREADNAME   = 0x0020,  
   BPREQI_PASSCOUNT    = 0x0040,  
   BPREQI_CONDITION    = 0x0080,  
   BPREQI_FLAGS        = 0x0100,  
   BPREQI_ALLOLDFIELDS = 0x01ff  
   BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only  
   BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only  
   BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only  
   BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only  
};  
```  
  
## <a name="members"></a>成员  
 BPREQI_BPLOCATION  
 初始化/使用 `bpLocation` [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 或 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构的 (断点位置) 字段。  
  
 BPREQI_LANGUAGE  
 初始化/使用 `guidLanguage` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_PROGRAM  
 初始化/使用 `pProgram` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_PROGRAMNAME  
 初始化/使用 `bstrProgramName` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_THREAD  
 初始化/使用 `pThread` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_THREADNAME  
 初始化/使用 `bstrThreadName` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_PASSCOUNT  
 初始化/使用 `bpPassCount` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_CONDITION  
 初始化/使用 `bpCondition` 或结构的 (断点条件) 字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_FLAGS  
 初始化/使用 `dwFlags` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI_ALLOLDFIELDS  
 初始化/使用结构的的所有字段 `BP_REQUEST_INFO` 。  
  
 BPREQI_VENDOR  
 初始化/使用 `guidVendor` 结构的字段 `BP_REQUEST_INFO2` 。  
  
 BPREQI_CONSTRAINT  
 初始化/使用 `bstrConstraint` 结构的字段 `BP_REQUEST_INFO2` 。  
  
 BPREQI_TRACEPOINT  
 初始化/使用 `bstrTracepoint` 结构的字段 `BP_REQUEST_INFO2` 。  
  
 BPREQI_ALLFIELDS  
 指定结构的所有字段 `BP_REQUEST_INFO2` 。  
  
## <a name="remarks"></a>备注  
 作为参数传递给 [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md) 和 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 方法，以指定要初始化 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 和 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构的哪些字段。  
  
 这些标志还用于指示在 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 返回每个结构时使用和结构的哪些字段。  
  
 这些值可以与按位组合 `OR` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
