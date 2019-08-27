---
title: IDebugDefaultPort2::GetPortNotify | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetPortNotify
helpviewer_keywords:
- IDebugDefaultPort2::GetPortNotify
ms.assetid: 3ae715ee-9886-4694-a52b-59bb3b27467a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd85f76ab0c882656ca79fe02296f30bdb83f523
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351766"
---
# <a name="idebugdefaultport2getportnotify"></a>IDebugDefaultPort2::GetPortNotify
此方法获取[IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)接口为此端口。

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
[out][IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 通常情况下，`QueryInterface`对象，实现上调用方法[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口，以获得[IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)接口。 但是，有一些情况下在不同的对象实现所需的接口。 此方法会隐藏这种情况，并返回`IDebugPortNotify2`中最合适的对象的接口。

## <a name="see-also"></a>请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)