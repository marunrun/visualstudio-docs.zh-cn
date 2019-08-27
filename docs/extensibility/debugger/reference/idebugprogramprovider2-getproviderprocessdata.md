---
title: IDebugProgramProvider2::GetProviderProcessData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bee54c3876c2de1be0754a74b429e6d24b80b738
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325029"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
检索从指定的进程正在运行的程序列表。

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

## <a name="parameters"></a>参数
`Flags`\
[in]中的标志的组合[PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)枚举。 下列标志则典型的此调用：

|Flag|描述|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|调用方在远程计算机上运行。|
|`PFLAG_DEBUGGEE`|当前正在调试调用方 （为每个节点将返回有关封送处理的其他信息）。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|调用方已附加到但不是启动调试器。|
|`PFLAG_GET_PROGRAM_NODES`|调用方要求提供程序节点的列表返回。|

`pPort`\
[in]调用进程的端口上运行。

`processId`\
[in][AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)保存包含该程序的进程的 ID 相关的结构。

`EngineFilter`\
[in]Guid 的数组，用于分配要调试该进程 （它们将用于筛选根据提供的引擎的支持; 如果未不指定任何引擎，则将返回所有程序实际都返回的程序） 的调试引擎。

`pProcess`\
[out]一个[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)填充所需的信息的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 一个过程来获取该进程中运行的程序的列表，通常情况下调用此方法。 返回的信息是一系列[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象。

## <a name="see-also"></a>请参阅
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)