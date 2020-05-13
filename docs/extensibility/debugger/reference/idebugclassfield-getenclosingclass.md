---
title: IDebugClassField：获取封闭类 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::GetEnclosingClass
helpviewer_keywords:
- IDebugClassField::GetEnclosingClass method
ms.assetid: a0c12e3c-9ea0-4dfb-9e45-8cea18725022
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e5a68e32da370d6881eb2b74cbca157f7b899329
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734392"
---
# <a name="idebugclassfieldgetenclosingclass"></a>IDebugClassField::GetEnclosingClass
获取包含此类的类。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEnclosingClass(
    IDebugClassField** ppClassField
);
```

```csharp
int GetEnclosingClass(
    out IDebugClassField ppClassField
);
```

## <a name="parameters"></a>参数
`ppClassField`\
[出]返回表示封闭类的[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)对象。 如果没有封闭类，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
如果此[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)对象表示的类是嵌套类，则`ppClassField`参数将返回表示封闭`IDebugClassField`类的对象。 例如，给定此类定义：

```
class RootClass {
    class NestedClass { }
};
```

在表示`GetEnclosingClass``IDebugClassField``NestedClass`类的对象上调用 方法返回表示类`IDebugClassField``RootClass`的对象。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
