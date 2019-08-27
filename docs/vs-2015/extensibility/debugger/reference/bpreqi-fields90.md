---
title: BPREQI_FIELDS90 | Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153206"
---
# <a name="bpreqifields90"></a>BPREQI_FIELDS90
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举指定断点请求有关的信息要检索的有效值。 此枚举扩展[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举。  
  
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
 初始化或使用`bpLocation`（断点位置） 的字段[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)或[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构。  
  
 BPREQI90_LANGUAGE  
 初始化或使用`guidLanguage`字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_PROGRAM  
 初始化或使用`pProgram`字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_PROGRAMNAME  
 初始化或使用`bstrProgramName`字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_THREAD  
 初始化或使用`pThread`字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_THREADNAME  
 初始化或使用`bstrThreadName`字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_PASSCOUNT  
 初始化或使用`bpPassCount`字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_CONDITION  
 初始化或使用`bpCondition`（断点条件） 字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_FLAGS  
 初始化或使用`dwFlags`字段`BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_ALLOLDFIELDS  
 初始化或使用的所有字段的`BP_REQUEST_INFO`结构。  
  
 BPREQI90_VENDOR  
 初始化或使用`guidVendor`字段的`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_CONSTRAINT  
 初始化或使用`bstrConstraint`字段的`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_TRACEPOINT  
 初始化或使用`bstrTracepoint`字段的`BP_REQUEST_INFO2`结构。  
  
 BPREQI90_MACROTRACEPOINT  
 初始化或使用`bstrMacroTracepoint`字段的`BP_REQUEST_INFO2`结构。 BPREQI_ALLFIELDS 不包括此字段。  
  
 BPREQI90_ALLFIELDS  
 指定的所有字段`BP_REQUEST_INFO2`结构。  
  
## <a name="requirements"></a>要求  
 标头：Msdbg90.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
