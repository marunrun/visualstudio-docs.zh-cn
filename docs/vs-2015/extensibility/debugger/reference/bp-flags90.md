---
title: BP_FLAGS90 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- BP_FLAGS90 enumeration
ms.assetid: 3e5a06c5-fb30-4b8a-b2d5-4a0570fc80bd
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9f7192eb7b2fa6d8bc886c0e601788ecba8eebcd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153493"
---
# <a name="bpflags90"></a>BP_FLAGS90
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举有效的可选标志值。 可选标志可能用于设置断点时指定的其他信息。 此枚举扩展[BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)枚举。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_BP_FLAGS90  
{  
   // VS 8.0 values  
   BP90_FLAG_NONE               = 0x0000,  
   BP90_FLAG_MAP_DOCPOSITION    = 0x0001,  
   BP90_FLAG_DONT_STOP          = 0x0002,  
  
   // Values added in VS 9.0  
   BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,  
};  
typedef DWORD BP_FLAGS90;  
```  
  
```csharp  
public enum enum_BP_FLAGS90  
{  
   // VS 8.0 values  
   BP90_FLAG_NONE                = 0x0000,  
   BP90_FLAG_MAP_DOCPOSITION     = 0x0001,  
   BP90_FLAG_DONT_STOP           = 0x0002,  
  
   // Values added in VS 9.0  
   BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,  
};  
```  
  
#### <a name="parameters"></a>参数  
 BP90_FLAG_NONE  
 不指定任何断点标志。  
  
 BP90_FLAG_MAP_DOCPOSITION  
 指定调试引擎 (DE) 应使用的文档位置的映射断点。 这是仅适用于面向脚本的源代码文件，如 Active Server Pages (ASP) 中设置断点。  
  
 BP90_FLAG_DONT_STOP  
 指定调试引擎中，应处理断点，但调试引擎最终应不停止进行控制。即[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)不应发送事件对象。 此标志用于主要与跟踪点一起使用。  
  
 BP90_FLAG_TRACEPOINT_CONTINUE  
 由本机调试引擎使用，以确定是否应该清除单步执行状态。 它不同于 BP90_FLAG_DONT_STOP 因为如果跟踪点执行宏，则不设置 BP90_FLAG_DONT_STOP。  
  
## <a name="requirements"></a>要求  
 标头：Msdbg90.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
