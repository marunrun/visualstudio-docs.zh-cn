---
title: IDebug程序提供程序2：：获取提供程序处理数据 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4e958900307f5f7915f58679709c88f80c2abfc9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721851"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
从指定进程检索正在运行的程序的列表。

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
[在][PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)枚举中的标志的组合。 以下标志是此调用的典型标志：

|标志|描述|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|呼叫者在远程计算机上运行。|
|`PFLAG_DEBUGGEE`|当前正在调试调用方（将为每个节点返回有关编组的其他信息）。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|调用方已附加到调试器，但未启动。|
|`PFLAG_GET_PROGRAM_NODES`|调用方要求返回程序节点的列表。|

`pPort`\
[在]调用进程正在运行的端口。

`processId`\
[在]包含包含相关程序的进程 ID 的[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构。

`EngineFilter`\
[在]分配给调试此过程的调试引擎的 GUID 数组（这些程序将用于筛选根据提供的引擎支持的内容实际返回的程序;如果未指定引擎，则将返回所有程序）。

`pProcess`\
[出]使用请求的信息填充[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)结构。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此过程通常调用此方法以获取该进程中运行的程序的列表。 返回的信息是[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象的列表。

## <a name="see-also"></a>请参阅
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
