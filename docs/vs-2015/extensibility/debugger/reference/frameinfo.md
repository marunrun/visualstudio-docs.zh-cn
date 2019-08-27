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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160166"
---
# <a name="frameinfo"></a>FRAMEINFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述一个堆栈帧。  
  
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
 中的标志的组合[FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)枚举，用于指定哪些字段填充。  
  
 m_bstrFuncName  
 与此堆栈帧关联的函数名称。  
  
 m_bstrReturnType  
 与此堆栈帧关联的返回类型。  
  
 m_bstrArgs  
 与此堆栈帧关联的函数的参数。  
  
 m_bstrLanguage  
 在其中实现该函数使用的语言。  
  
 m_bstrModule  
 与此堆栈帧关联的模块名称。  
  
 m_addrMin  
 最小物理堆栈地址中。  
  
 m_addrMAX  
 最大物理堆栈地址中。  
  
 m_pFrame  
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)对象，表示此堆栈帧。  
  
 m_pFrame  
 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)对象，表示包含此堆栈帧的模块。  
  
 m_fHasDebugInfo  
 非零 (`TRUE`) 如果给定范围中存在的调试信息。  
  
 m_fHasDebugInfo  
 非零 (`TRUE`) 将不再有效的代码与关联的堆栈帧时。  
  
 m_fHasDebugInfo  
 非零 (`TRUE`) 如果会话调试管理器 (SDM) 进行批注的堆栈帧。  
  
## <a name="remarks"></a>备注  
 此结构传递给[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)要填充的方法。 此结构也包含在一个列表，其中包含在[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)接口，反过来，通过调用将返回该值[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)方法。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)   
 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)   
 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
