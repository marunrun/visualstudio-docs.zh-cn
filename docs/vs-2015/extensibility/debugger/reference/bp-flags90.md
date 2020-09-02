---
title: BP_FLAGS90 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153493"
---
# <a name="bp_flags90"></a>BP_FLAGS90
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举可选标志的有效值。 设置断点时，可以使用可选标志来指定其他信息。 此枚举扩展 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) 枚举。  
  
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
 指定无断点标志。  
  
 BP90_FLAG_MAP_DOCPOSITION  
 指定调试引擎 (DE) 应使用文档位置映射断点。 这仅适用于在面向脚本的源文件中设置的断点，例如 (ASP) 的 Active Server Pages。  
  
 BP90_FLAG_DONT_STOP  
 指定应由调试引擎处理断点，但调试引擎最终不应在该处停止;也就是说，不应发送 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) 事件对象。 此标志旨在主要用于跟踪点。  
  
 BP90_FLAG_TRACEPOINT_CONTINUE  
 由本机调试引擎用来确定是否应清除步进状态。 它与 BP90_FLAG_DONT_STOP 不同，因为如果跟踪点执行宏，则不设置 BP90_FLAG_DONT_STOP。  
  
## <a name="requirements"></a>要求  
 标头： Msdbg90  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
