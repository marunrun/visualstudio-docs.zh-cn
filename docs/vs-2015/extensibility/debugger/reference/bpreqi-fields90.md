---
title: BPREQI_FIELDS90 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- BPREQI_FIELDS90 enumeration
ms.assetid: bf6f7efc-39f2-46a2-906d-c3647bf89995
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 97a38b4296668cb287f34e5b1afcbd7c90477011
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153206"
---
# <a name="bpreqi_fields90"></a>BPREQI_FIELDS90
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举有效的值，该值指定要检索的有关断点请求的信息。 此枚举扩展 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) 枚举。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_BPREQI_FIELDS90  
{  
   // VS 8.0 values  
   BPREQI90_BPLOCATION                = 0x0001,  
   BPREQI90_LANGUAGE                  = 0x0002,  
   BPREQI90_PROGRAM                   = 0x0004,  
   BPREQI90_PROGRAMNAME               = 0x0008,  
   BPREQI90_THREAD                    = 0x0010,  
   BPREQI90_THREADNAME                = 0x0020,  
   BPREQI90_PASSCOUNT                 = 0x0040,  
   BPREQI90_CONDITION                 = 0x0080,  
   BPREQI90_FLAGS                     = 0x0100,  
   BPREQI90_ALLOLDFIELDS              = 0x01ff,  
   BPREQI90_VENDOR                    = 0x0200,  
   BPREQI90_CONSTRAINT                = 0x0400,  
   BPREQI90_TRACEPOINT                = 0x0800,  
  
   // Values added in VS 9.0  
   BPREQI90_MACROTRACEPOINT           = 0x1000,  
  
   BPREQI90_ALLFIELDS                 = 0xffff  
};  
typedef DWORD BPREQI_FIELDS90;  
```  
  
```csharp  
public enum enum_BPREQI_FIELDS90  
{  
    // VS 8.0 values  
    BPREQI90_BPLOCATION                = 0x0001,  
    BPREQI90_LANGUAGE                  = 0x0002,  
    BPREQI90_PROGRAM                   = 0x0004,  
    BPREQI90_PROGRAMNAME               = 0x0008,  
    BPREQI90_THREAD                    = 0x0010,  
    BPREQI90_THREADNAME                = 0x0020,  
    BPREQI90_PASSCOUNT                 = 0x0040,  
    BPREQI90_CONDITION                 = 0x0080,  
    BPREQI90_FLAGS                     = 0x0100,  
    BPREQI90_ALLOLDFIELDS              = 0x01ff,  
    BPREQI90_VENDOR                    = 0x0200,  
    BPREQI90_CONSTRAINT                = 0x0400,  
    BPREQI90_TRACEPOINT                = 0x0800,  
  
    // Values added in VS 9.0  
    BPREQI90_MACROTRACEPOINT           = 0x1000,  
  
    BPREQI90_ALLFIELDS                 = 0xffff  
};  
```  
  
#### <a name="parameters"></a>参数  
 BPREQI90_BPLOCATION  
 初始化或使用 `bpLocation` [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 或 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构的 (断点位置) 字段。  
  
 BPREQI90_LANGUAGE  
 初始化或使用 `guidLanguage` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_PROGRAM  
 初始化或使用 `pProgram` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_PROGRAMNAME  
 初始化或使用 `bstrProgramName` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_THREAD  
 初始化或使用 `pThread` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_THREADNAME  
 初始化或使用 `bstrThreadName` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_PASSCOUNT  
 初始化或使用 `bpPassCount` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_CONDITION  
 初始化或使用 `bpCondition` 或结构的 (断点条件) 字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_FLAGS  
 初始化或使用 `dwFlags` 或结构的字段 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 。  
  
 BPREQI90_ALLOLDFIELDS  
 初始化或使用结构的的所有字段 `BP_REQUEST_INFO` 。  
  
 BPREQI90_VENDOR  
 初始化或使用 `guidVendor` 结构的字段 `BP_REQUEST_INFO2` 。  
  
 BPREQI90_CONSTRAINT  
 初始化或使用 `bstrConstraint` 结构的字段 `BP_REQUEST_INFO2` 。  
  
 BPREQI90_TRACEPOINT  
 初始化或使用 `bstrTracepoint` 结构的字段 `BP_REQUEST_INFO2` 。  
  
 BPREQI90_MACROTRACEPOINT  
 初始化或使用 `bstrMacroTracepoint` 结构的字段 `BP_REQUEST_INFO2` 。 BPREQI_ALLFIELDS 不包括此字段。  
  
 BPREQI90_ALLFIELDS  
 指定结构的所有字段 `BP_REQUEST_INFO2` 。  
  
## <a name="requirements"></a>要求  
 标头： Msdbg90  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
