---
title: PROVIDER_FLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PROVIDER_FLAGS
helpviewer_keywords:
- PROVIDER_FLAGS enumeration
ms.assetid: 8cbd2312-ed2f-4477-b192-c3f25c6098c3
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c39aa316308f313bf23ef2c5680671585636f0a5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204939"
---
# <a name="providerflags"></a>PROVIDER_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要从程序提供程序获取所需的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp  
enum enum_PROVIDER_FLAGS {  
   PFLAG_NONE                    = 0x00,  
   PFLAG_REMOTE_PORT             = 0x01,  
   PFLAG_DEBUGGEE                = 0x02,  
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,  
   PFLAG_REASON_WATCH            = 0x08,  
   PFLAG_GET_PROGRAM_NODES       = 0x10,  
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20  
};  
typedef DWORD PROVIDER_FLAGS;  
```  
  
```csharp  
public enum enum_PROVIDER_FLAGS {  
   PFLAG_NONE                    = 0x00,  
   PFLAG_REMOTE_PORT             = 0x01,  
   PFLAG_DEBUGGEE                = 0x02,  
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,  
   PFLAG_REASON_WATCH            = 0x08,  
   PFLAG_GET_PROGRAM_NODES       = 0x10,  
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20  
};  
```  
  
## <a name="members"></a>成员  
 PFLAG_NONE  
 指定任何标志。  
  
 PFLAG_REMOTE_PORT  
 调用方想以外的其他计算机上的程序列表[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]。  
  
 PFLAG_DEBUGGEE  
 进程当前正在调试的此实例[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]。  
  
 PFLAG_ATTACH_TODEBUGGEE  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 附加到正在调试的程序，但未启动。  
  
 PFLAG_REASON_WATCH  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 正在监视的事件。  
  
 PFLAG_GET_PROGRAM_NODES  
 调用方想`ProgramNodes`字段[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)结构。  
  
 PFLAG_GET_IS_DEBUGGER_PRESENT  
 调用方想`fIsTheDebuggerPresent`字段的`PROVIDER_PROCESS_DATA`结构。  
  
## <a name="remarks"></a>备注  
 这些标志将传递到以下方法：  
  
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)  
  
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)  
  
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)  
  
  可以组合这些值的按位`OR`。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)   
 [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)   
 [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)   
 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
