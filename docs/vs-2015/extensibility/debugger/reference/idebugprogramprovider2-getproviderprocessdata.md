---
title: IDebugProgramProvider2：： GetProviderProcessData |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a50faf4531a098dde544adcffe535ed26e9c5cd8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148520"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索指定进程中正在运行的程序的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetProviderProcessData(  
   PROVIDER_FLAGS         Flags,  
   IDebugDefaultPort2*    pPort,  
   AD_PROCESS_ID          processId,  
   CONST_GUID_ARRAY       EngineFilter,  
   PROVIDER_PROCESS_DATA* pProcess  
);  
```  
  
```csharp  
int GetProviderProcessData(  
   enum_PROVIDER_FLAGS     Flags,  
   IDebugDefaultPort2      pPort,  
   AD_PROCESS_ID           ProcessId,  
   CONST_GUID_ARRAY        EngineFilter,  
   PROVIDER_PROCESS_DATA[] pProcess  
);  
```  
  
#### <a name="parameters"></a>参数  
 `Flags`  
 中 [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) 枚举中的标志的组合。 下面是此调用的典型标志：  
  
|标志|描述|  
|----------|-----------------|  
|`PFLAG_REMOTE_PORT`|调用方正在远程计算机上运行。|  
|`PFLAG_DEBUGGEE`|当前正在调试调用方 (将为每个节点) 返回有关封送的附加信息。|  
|`PFLAG_ATTACHED_TO_DEBUGGEE`|调用方已附加到，但调试器未启动。|  
|`PFLAG_GET_PROGRAM_NODES`|调用方正在请求返回要返回的程序节点的列表。|  
  
 `pPort`  
 中正在运行调用进程的端口。  
  
 `processId`  
 中一个 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 结构，它保存包含相关程序的进程的 ID。  
  
 `EngineFilter`  
 中为调试引擎分配的 Guid 的数组，这些 Guid 用于调试此进程 (它们将用于根据提供的引擎支持的功能筛选实际返回的程序;如果未指定引擎，将) 返回所有程序。  
  
 `pProcess`  
 弄使用请求的信息填充的 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) 结构。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法通常由进程调用，以获取在该进程中运行的程序的列表。 返回的信息是 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象的列表。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)   
 [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)   
 [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)   
 [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)   
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
