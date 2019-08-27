---
title: IEnumDebugProcesses2::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2::Next
helpviewer_keywords:
- IEnumDebugProcesses2::Next
ms.assetid: abef89eb-198b-49cd-a4c9-17bce6cac0e1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 734be605517adf4e127a7f1f936fb799449ce467
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326185"
---
# <a name="ienumdebugprocesses2next"></a>IEnumDebugProcesses2::Next
枚举中返回下一组元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG            celt,
   IDebugProcess2** rgelt,
   ULONG*           pceltFetched
);
```

```csharp
int Next(
   uint             celt,
   IDebugProcess2[] rgelt,
   ref uint         pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要检索的元素数。 此外可以指定的最大大小`rgelt`数组。

`rgelt`\
[in、 out]数组[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)要填充的元素。

`pceltFetched`\
[out]返回中实际返回的元素数目`rgelt`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果无法返回请求的元素数少于; 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)