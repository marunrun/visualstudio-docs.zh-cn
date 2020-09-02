---
title: BP_REQUEST_INFO2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65edef6585fd8367c6fb23c291bf4e8376de8861
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153351"
---
# <a name="bp_request_info2"></a>BP_REQUEST_INFO2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

包含实现断点所需的信息，包括供应商 GUID、约束和跟踪点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _BP_REQUEST_INFO2 {  
   BPREQI_FIELDS   dwFields;  
   GUID            guidLanguage;  
   BP_LOCATION     bpLocation;  
   IDebugProgram2* pProgram;  
   BSTR            bstrProgramName;  
   IDebugThread2*  pThread;  
   BSTR            bstrThreadName;  
   BP_CONDITION    bpCondition;  
   BP_PASSCOUNT    bpPassCount;  
   BP_FLAGS        dwFlags;  
   GUID            guidVendor;  
   BSTR            bstrConstraint;  
   BSTR            bstrTracepoint;  
} BP_REQUEST_INFO2;  
```  
  
```csharp  
public struct BP_REQUEST_INFO2 {  
   public uint           dwFields;  
   public Guid           guidLanguage;  
   public BP_LOCATION    bpLocation;  
   public IDebugProgram2 pProgram;  
   public string         bstrProgramName;  
   public IDebugThread2  pThread;  
   public string         bstrThreadName;  
   public BP_CONDITION   bpCondition;  
   public BP_PASSCOUNT   bpPassCount;  
   public uint           dwFlags;  
   public Guid           guidVendor;  
   public string         bstrConstraint;  
   public string         bstrTracepoint;  
};  
```  
  
## <a name="members"></a>成员  
 `dwFields`  
 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举中的标志的组合，用于指定要填写的字段。  
  
 `guidLanguage`  
 语言 GUID。  
  
 `bpLocation`  
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构，它指定断点位置的类型。  
  
 `pProgram`  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示在其中发生断点的应用程序。  
  
 `bstrProgramName`  
 发生断点的应用程序的名称。  
  
 `pThread`  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示在其中发生断点的线程。  
  
 `bstrThreadName`  
 发生断点的线程的名称。  
  
 `bpCondition`  
 描述引发断点的条件的 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 结构。  
  
 `bpPassCount`  
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构，它包含断点的传递计数信息。  
  
 `dwFlags`  
 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)枚举中的标志的组合，该枚举指定请求的断点的标志。  
  
 `guidVendor`  
 供应商的 GUID。 可以为 null 值。  
  
 `bstrConstraint`  
 断点约束的名称。 可以为 null 值。  
  
 `bstrTracepoint`  
 跟踪点的名称。 可以为 null 值。  
  
## <a name="remarks"></a>备注  
 此结构由 [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md) 方法返回。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)   
 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)   
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)   
 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
