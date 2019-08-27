---
title: PROCESS_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PROCESS_INFO
helpviewer_keywords:
- PROCESS_INFO structure
ms.assetid: 260c33cc-a05e-4645-84b6-536d0b3b0537
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9ab05d85b55fd293b648603f067d135f703aff5e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205023"
---
# <a name="processinfo"></a>PROCESS_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

包含有关进程的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct tagPROCESS_INFO {   
   PROCESS_INFO_FIELDS Fields;  
   BSTR                bstrFileName;  
   BSTR                bstrBaseName;  
   BSTR                bstrTitle;  
   AD_PROCESS_ID       ProcessId;  
   DWORD               dwSessionId;  
   BSTR                bstrAttachedSessionName;  
   FILETIME            CreationTime;  
   PROCESS_INFO_FLAGS  Flags;  
} PROCESS_INFO;  
```  
  
```csharp  
public struct PROCESS_INFO {   
   public uint          Fields;  
   public string        bstrFileName;  
   public string        bstrBaseName;  
   public string        bstrTitle;  
   public AD_PROCESS_ID ProcessId;  
   public uint          dwSessionId;  
   public string        bstrAttachedSessionName;  
   public FILETIME      CreationTime;  
   public uint          Flags;  
};  
```  
  
## <a name="members"></a>成员  
 字段  
 中的标志的组合[PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)枚举，用于指定哪些字段填写。  
  
 bstrFileName  
 过程的完整路径名称。 等效于调用[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)方法及参数`GN_FILENAME`。  
  
 bstrBaseName  
 文件的名称和进程的扩展。 等效于调用`IDebugProcess2::Getname`方法及参数`GN_BASENAME`。  
  
 bstrTitle  
 此过程中，如果存在的标题。 等效于调用`IDebugProcess2::Getname`方法及参数`GN_TITLE`。  
  
 ProcessId  
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)标识进程的结构。 等效于调用[GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)方法。  
  
 dwSessionId  
 调试会话中运行此进程的标识符。  
  
 bstrAttachedSessionName  
 附加的会话名称。 等效于调用[GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)方法。  
  
 CreationTime  
 创建过程的时间。  
  
 Flags  
 中的标志的组合[PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)指定进程的属性的枚举。  
  
## <a name="remarks"></a>备注  
 此结构传递给[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)填写其中的方法。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)   
 [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)   
 [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)   
 [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)   
 [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)
