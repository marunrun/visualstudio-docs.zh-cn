---
title: FRAMEINFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- FRAMEINFO
helpviewer_keywords:
- FRAMEINFO structure
ms.assetid: 95001b89-dddb-45bb-889d-8327994e38a5
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c0fa2299e47924a10a6d0b02a982535865164191
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160166"
---
# <a name="frameinfo"></a>FRAMEINFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct tagFRAMEINFO {   
   FRAMEINFO_FLAGS    m_dwValidFields;  
   BSTR               m_bstrFuncName;  
   BSTR               m_bstrReturnType;  
   BSTR               m_bstrArgs;  
   BSTR               m_bstrLanguage;  
   BSTR               m_bstrModule;  
   UINT64             m_addrMin;  
   UINT64             m_addrMax;  
   IDebugStackFrame2* m_pFrame;  
   IDebugModule2*     m_pModule;  
   BOOL               m_fHasDebugInfo;  
   BOOL               m_fStaleCode;  
   BOOL               m_fAnnotatedFrame;  
} FRAMEINFO;  
```  
  
```csharp  
public struct FRAMEINFO {   
   public uint              m_dwValidFields;  
   public string            m_bstrFuncName;  
   public string            m_bstrReturnType;  
   public string            m_bstrArgs;  
   public string            m_bstrLanguage;  
   public string            m_bstrModule;  
   public ulong             m_addrMin;  
   public ulong             m_addrMax;  
   public IDebugStackFrame2 m_pFrame;  
   public IDebugModule2     m_pModule;  
   public int               m_fHasDebugInfo;  
   public int               m_fStaleCode;  
   public int               m_fAnnotatedFrame;  
} FRAMEINFO;  
```  
  
## <a name="members"></a>成员  
 m_dwValidFields  
 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)枚举中的标志的组合，用于指定要填写的字段。  
  
 m_bstrFuncName  
 与堆栈帧关联的函数名称。  
  
 m_bstrReturnType  
 与堆栈帧关联的返回类型。  
  
 m_bstrArgs  
 与堆栈帧关联的函数的参数。  
  
 m_bstrLanguage  
 实现该函数所用的语言。  
  
 m_bstrModule  
 与堆栈帧关联的模块名称。  
  
 m_addrMin  
 最小物理堆栈地址。  
  
 m_addrMAX  
 最大物理堆栈地址。  
  
 m_pFrame  
 表示此堆栈帧的 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 对象。  
  
 m_pFrame  
 表示包含此堆栈帧的模块的 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) 对象。  
  
 m_fHasDebugInfo  
 `TRUE`如果给定帧中存在调试信息，则为非零 () 。  
  
 m_fHasDebugInfo  
 `TRUE`如果堆栈帧与不再有效的代码相关联，则为非零 () 。  
  
 m_fHasDebugInfo  
 `TRUE`如果堆栈帧由会话调试管理器 (SDM) 进行批注，则为非零 () 。  
  
## <a name="remarks"></a>备注  
 此结构传递到要填写的 [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md) 方法。 此结构还包含在 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) 接口中，后者又会从对 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) 方法的调用返回。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)   
 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)   
 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
