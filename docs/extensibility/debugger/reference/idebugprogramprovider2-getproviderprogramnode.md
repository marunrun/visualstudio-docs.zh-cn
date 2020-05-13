---
title: IDebug程序提供程序2：：获取提供程序程序节点 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProgramNode
ms.assetid: e62e8e83-acbb-4c52-aedf-ffbd4670db29
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd8ca7d5120ba20695caef2e9021ee25869df72f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721805"
---
# <a name="idebugprogramprovider2getproviderprogramnode"></a>IDebugProgramProvider2::GetProviderProgramNode
检索特定程序的程序节点。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProviderProgramNode(
   PROVIDER_FLAGS       Flags,
   IDebugDefaultPort2*  pPort,
   AD_PROCESS_ID        processId,
   REFGUID              guidEngine,
   UINT64               programId,
   IDebugProgramNode2** ppProgramNode
);
```

```csharp
int GetProviderProgramNode(
   enum_PROVIDER_FLAGS    Flags,
   IDebugDefaultPort2     pPort,
   AD_PROCESS_ID          ProcessId,
   ref Guid               guidEngine,
   ulong                  programId,
   out IDebugProgramNode2 ppProgramNode
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

`pPort`\
[在]调用进程正在运行的端口。

`processId`\
[在]包含包含相关程序的进程 ID 的[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构。

`guidEngine`\
[在]程序附加到的调试引擎的 GUID（如果有）。

`programId`\
[在]要为其获取程序节点的程序的 ID。

`ppProgramNode`\
[出]表示请求的程序节点的[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
