---
title: IDebugDefaultPort2：： GetPortNotify |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetPortNotify
helpviewer_keywords:
- IDebugDefaultPort2::GetPortNotify
ms.assetid: 3ae715ee-9886-4694-a52b-59bb3b27467a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 670dd128e6962c1e1d12f81eea03f9759fa56621
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80732402"
---
# <a name="idebugdefaultport2getportnotify"></a>IDebugDefaultPort2::GetPortNotify
此方法获取此端口的 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPortNotify(
   IDebugPortNotify2** ppPortNotify
);
```

```csharp
int GetPortNotify(
   out IDebugPortNotify2 ppPortNotify
);
```

## <a name="parameters"></a>参数
`ppPortNotify`\
弄一个 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 通常，对 `QueryInterface` 实现 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 接口的对象调用方法以获取 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 接口。 但是，在某些情况下，需要在不同的对象上实现所需的接口。 此方法隐藏这些情况并 `IDebugPortNotify2` 从最适当的对象返回接口。

## <a name="see-also"></a>另请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
