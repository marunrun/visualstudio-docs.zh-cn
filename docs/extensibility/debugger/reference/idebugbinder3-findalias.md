---
title: IDebugBinder3：：查找别名 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f0a697e39d21b1c25a98c09ad6cc4837cca7a293
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735859"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
此方法定位一个别名，给定一个名称。 这将搜索程序中的所有别名。

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
[在]要查找的别名的名称。

`ppAlias`\
[出]找到（如果有）由[IDebugAlias 接口](../../../extensibility/debugger/reference/idebugalias.md)表示的别名。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回`S_FALSE`（如果未找到别名）或错误代码。

## <a name="remarks"></a>备注
 此方法在调用之前将目标对象初始化为 null;然后，它会在之后测试一个空值，以确定是否找到别名。

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
