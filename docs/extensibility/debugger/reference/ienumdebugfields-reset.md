---
title: IEnum调试字段：重置 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Reset
helpviewer_keywords:
- IEnumDebugFields::Reset method
ms.assetid: 38ff61e4-0120-42e8-971a-16be6050b425
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be33249ef583776f613c6716143249e3ce31bc8d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716845"
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
 无

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，下一个调用[Next](../../../extensibility/debugger/reference/ienumdebugfields-next.md)将返回枚举的第一个元素。

## <a name="see-also"></a>请参阅
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [下一步](../../../extensibility/debugger/reference/ienumdebugfields-next.md)
