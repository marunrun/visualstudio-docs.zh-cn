---
title: IEnum调试对象：：获取计数 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects::GetCount
helpviewer_keywords:
- IEnumDebugObjects::GetCount method
ms.assetid: 9cbc5db4-03ae-479f-a664-13cad66ad210
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1475652e340ff793dc900ab11563c0c1ad82c9b1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716351"
---
# <a name="ienumdebugobjectsgetcount"></a>IEnumDebugObjects::GetCount
此方法返回枚举中的元素数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCount(
   [out] ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
[出]返回枚举中的元素数。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法不是习惯的 COM 枚举接口的一部分，该接口指定仅实现"下一步"、克隆、跳过和重置。

## <a name="see-also"></a>请参阅
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
