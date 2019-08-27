---
title: IDebugMethodField::GetGlobalContainer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetGlobalContainer
helpviewer_keywords:
- IDebugMethodField::GetGlobalContainer method
ms.assetid: 041ac5aa-0b80-4310-b9ae-b88f8e7e0e5f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 77f3d82beab43b227dd3beb772dd41353d89b6fe
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324177"
---
# <a name="idebugmethodfieldgetglobalcontainer"></a>IDebugMethodField::GetGlobalContainer
获取方法的全局容器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetGlobalContainer(
   IDebugClassField** ppClass
);
```

```csharp
int GetGlobalContainer(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>参数
`ppClass`\
[out]返回[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)表示在其中定义此方法的模块。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 返回[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)对象表示整个模块，是一个自定义对象，也就是说，对模块自身不具有实际类但可由表示`IDebugClassField`对象，并且允许各种要进行枚举和发现的模块的元素。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)