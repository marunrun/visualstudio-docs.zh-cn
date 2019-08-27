---
title: IDebugEngine3::SetEngineGuid | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetEngineGuid
helpviewer_keywords:
- IDebugEngine3::SetEngineGuid
ms.assetid: 8bdfa05d-feb7-4d98-abac-77825a04c50f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 66b72edc81cdde1d3d83e4c3534b50e40dd2cf19
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352489"
---
# <a name="idebugengine3setengineguid"></a>IDebugEngine3::SetEngineGuid
此方法设置调试引擎 (DE) `GUID`。

## <a name="syntax"></a>语法

```cpp
HRESULT SetEngineGuid(
   GUID* guidEngine
);
```

```csharp
int SetEngineGuid(
   ref Guid guidEngine
);
```

## <a name="parameters"></a>参数
`guidEngine`\
[in]`GUID`的引擎。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)