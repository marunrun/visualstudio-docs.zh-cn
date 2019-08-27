---
title: IDebugCoreServer3::DisableAutoAttach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::DisableAutoAttach
helpviewer_keywords:
- IDebugCoreServer3::DisableAutoAttach
ms.assetid: 9d860a20-c154-4df4-ba15-636e0fcd42bf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 52d92cdfbbf076a733cacba307d30fe2006a4fc6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317753"
---
# <a name="idebugcoreserver3disableautoattach"></a>IDebugCoreServer3::DisableAutoAttach
禁用自动附加与此服务器关联的所有调试引擎。

## <a name="syntax"></a>语法

```cpp
HRESULT DisableAutoAttach(
   void
);
```

```csharp
int DisableAutoAttach();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)