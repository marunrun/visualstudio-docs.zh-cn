---
title: IDebugCoreServer3::DiagnoseWebDebuggingError |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
helpviewer_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
ms.assetid: 8c4570ca-ae55-42f2-bbaa-8d8e75d2fa19
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 52b6d634da7cda9c7b90b8cd4f7d93e7accc033d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317787"
---
# <a name="idebugcoreserver3diagnosewebdebuggingerror"></a>IDebugCoreServer3::DiagnoseWebDebuggingError
若要确定原因 auto-attach 的尝试失败。

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
[in]当前未使用;始终应设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 以下是其他典型的返回代码：

|代码|描述|
|----------|-----------------|
|`S_WEBDBG_UNABLE_TO_DIAGNOSE`|无法确定远程服务器启动调试失败的原因。|
|`S_WEBDBG_DEBUG_VERB_BLOCKED`|无法调试在远程服务器上，可能是由于权限不足，或者是因为未启用 DEBUG 谓词。|
|`E_WEBDBG_DEBUG_VERB_BLOCKED`|Web 服务器已被锁定，并阻止 DEBUG 谓词，用于以启用调试。|

## <a name="see-also"></a>请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)