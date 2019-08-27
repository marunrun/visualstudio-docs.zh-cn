---
title: IDebugBinder3::FindAlias |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8387a3302395d6e25c2b00dd360286e533531168
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344419"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
此方法可查找给定名称的别名。 这将在程序中搜索所有别名。

## <a name="syntax"></a>语法

```cpp
HRESULT FindAlias(
   LPCOLESTR     pcstrName,
   IDebugAlias** ppAlias
);
```

```csharp
int FindAlias(
   string          pcstrName,
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>参数
`pcstrName`\
[in]若要查找的别名的名称。

`ppAlias`\
[out]别名找到 （如果有） 由[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)接口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`（如果找不到别名） 或错误代码。

## <a name="remarks"></a>备注
 此方法将目标对象初始化为 null 之前，调用;然后它测试 null 值之后，若要确定找到该别名。

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)