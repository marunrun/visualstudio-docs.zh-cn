---
title: IDebugEngineCreateEvent2：： GetEngine |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineCreateEvent2::GetEngine
helpviewer_keywords:
- IDebugEngineCreateEvent2::GetEngine
ms.assetid: 187d24ed-9f9a-4418-a0ef-b8a19f54652c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 57e2eca3506bf965ca51b76c35d3e677ac21d80b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730616"
---
# <a name="idebugenginecreateevent2getengine"></a>IDebugEngineCreateEvent2::GetEngine
检索表示新创建的调试引擎 (DE) 的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngine( 
   IDebugEngine2** pEngine
);
```

```csharp
int GetEngine( 
   out IDebugEngine2 pEngine
);
```

## <a name="parameters"></a>参数
`pEngine`\
弄返回一个 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 对象，该对象表示新创建的 DE。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
