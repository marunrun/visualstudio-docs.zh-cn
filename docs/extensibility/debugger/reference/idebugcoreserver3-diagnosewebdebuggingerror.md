---
title: IDebugCoreServer3：:Diagnose网络调试错误 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
helpviewer_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
ms.assetid: 8c4570ca-ae55-42f2-bbaa-8d8e75d2fa19
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fec5b8fbe1cae18b8221702fe14443df231d8880
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732947"
---
# <a name="idebugcoreserver3diagnosewebdebuggingerror"></a>IDebugCoreServer3::DiagnoseWebDebuggingError
尝试确定自动附加失败的原因。

## <a name="syntax"></a>语法

```cpp
HRESULT DiagnoseWebDebuggingError(
   LPCWSTR pszUrl
);
```

```csharp
int DiagnoseWebDebuggingError(
   string pszUrl
);
```

## <a name="parameters"></a>参数
`pszUrl`\
[在]当前未使用;应始终设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 以下是其他典型的退货代码：

|代码|描述|
|----------|-----------------|
|`S_WEBDBG_UNABLE_TO_DIAGNOSE`|无法确定远程服务器无法启动调试的原因。|
|`S_WEBDBG_DEBUG_VERB_BLOCKED`|无法在远程服务器上调试，可能是由于权限不足或未启用 DEBUG 谓词。|
|`E_WEBDBG_DEBUG_VERB_BLOCKED`|Web 服务器已锁定并阻止启用调试所需的 DEBUG 谓词。|

## <a name="see-also"></a>请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
