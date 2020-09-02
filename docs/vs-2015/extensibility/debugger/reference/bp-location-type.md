---
title: BP_LOCATION_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_TYPE
helpviewer_keywords:
- BP_LOCATION_TYPE structure
ms.assetid: 0248430a-3b61-4809-87a9-e9b6bb7d1130
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fb8074317e52b43806a61d6486c53d7409333e2c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153407"
---
# <a name="bp_location_type"></a>BP_LOCATION_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定断点请求的断点的位置类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_BP_LOCATION_TYPE {   
   BPLT_NONE               = 0x00000000,  
   BPLT_FILE_LINE          = 0x00010000,  
   BPLT_FUNC_OFFSET        = 0x00020000,  
   BPLT_CONTEXT            = 0x00030000,  
   BPLT_STRING             = 0x00040000,  
   BPLT_ADDRESS            = 0x00050000,  
   BPLT_RESOLUTION         = 0x00060000,  
   BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,  
   BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,  
   BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,  
   BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,  
   BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,  
   BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,  
   BPLT_TYPE_MASK          = 0x0000FFFF,  
   BPLT_LOCATION_TYPE_MASK = 0xFFFF0000  
};  
typedef DWORD BP_LOCATION_TYPE;  
```  
  
```csharp  
public enum enum_BP_LOCATION_TYPE {   
   BPLT_NONE               = 0x00000000,  
   BPLT_FILE_LINE          = 0x00010000,  
   BPLT_FUNC_OFFSET        = 0x00020000,  
   BPLT_CONTEXT            = 0x00030000,  
   BPLT_STRING             = 0x00040000,  
   BPLT_ADDRESS            = 0x00050000,  
   BPLT_RESOLUTION         = 0x00060000,  
   BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,  
   BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,  
   BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,  
   BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,  
   BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,  
   BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,  
   BPLT_TYPE_MASK          = 0x0000FFFF,  
   BPLT_LOCATION_TYPE_MASK = 0xFFFF0000  
};  
```  
  
## <a name="members"></a>成员  
 BPLT_NONE  
 指定无断点位置。  
  
 BPLT_FILE_LINE  
 以文件行形式指定断点的位置类型。  
  
 BPLT_FUNC_OFFSET  
 指定断点的位置类型作为函数偏移量。  
  
 BPLT_CONTEXT  
 指定断点的位置类型作为上下文。  
  
 BPLT_STRING  
 以字符串的形式指定断点的位置类型。  
  
 BPLT_ADDRESS  
 指定断点的位置类型作为地址。  
  
 BPLT_RESOLUTION  
 指定断点的位置类型作为解析。  
  
 BPLT_CODE_FILE_LINE  
 以源代码行的形式指定断点的位置类型。  
  
 BPLT_CODE_FUNC_OFFSET  
 指定断点的位置类型作为代码函数偏移量。  
  
 BPLT_CODE_CONTEXT  
 将断点的位置类型指定为代码上下文。  
  
 BPLT_CODE_STRING  
 指定断点的位置类型作为代码字符串。  
  
 BPLT_CODE_ADDRESS  
 指定断点的位置类型作为代码地址。  
  
 BPLT_DATA_STRING  
 指定断点的位置类型作为数据字符串。  
  
 BPLT_TYPE_MASK  
 指定位掩码，以便可以从值中提取断点类型。  
  
 BPLT_LOCATION_TYPE_MASK  
 指定位掩码，以便可以从值中提取断点位置类型。  
  
## <a name="remarks"></a>备注  
 作为参数传递给 [GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md) 方法。  
  
 断点位置类型由断点类型和位置类型组成。 这意味着，断点位置类型永远不会只是断点类型 (例如 `BPT_CODE`) 或位置类型 (例如 `BPLT_FILE_LINE`) 。 当前支持的所有断点位置类型的预定义常量都包含在此枚举 (`BPLT_CODE_FILE_LINE` 通过 `BPLT_DATA_STRING`) 。  
  
 `BPT_CODE` 和 `BPT_DATA` 是 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) 枚举的成员。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)   
 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
