---
title: IEnumDebugFields::Reset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Reset
helpviewer_keywords:
- IEnumDebugFields::Reset method
ms.assetid: 38ff61e4-0120-42e8-971a-16be6050b425
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c50a5e2ed55bf1550ca4a70bc566fb2504b100a3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350418"
---
# <a name="ienumdebugfieldsreset"></a>IEnumDebugFields::Reset
此方法将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

#### <a name="parameters"></a>参数
 None

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 调用此方法下, 一步调用后[下一步](../../../extensibility/debugger/reference/ienumdebugfields-next.md)返回枚举的第一个元素。

## <a name="see-also"></a>请参阅
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugfields-next.md)