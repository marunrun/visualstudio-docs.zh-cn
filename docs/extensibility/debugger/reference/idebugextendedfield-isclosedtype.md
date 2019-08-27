---
title: IDebugExtendedField::IsClosedType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IsClosedType
- IDebugExtendedField::IsClosedType
ms.assetid: 9136fc57-74ff-4fe4-a6e2-b137cb9d5b08
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0ea8e501d338de24a49b04a61b46652c062a027a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352689"
---
# <a name="idebugextendedfieldisclosedtype"></a>IDebugExtendedField::IsClosedType
确定是否该字段表示封闭的类型。

## <a name="syntax"></a>语法

```cpp
HRESULT IsClosedType(
   void
);
```

```csharp
int IsClosedType();
```

## <a name="return-value"></a>返回值
 如果此字段为关闭的类型，则返回`S_OK`; 否则为返回`S_FALSE`。

## <a name="see-also"></a>请参阅
- [IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)