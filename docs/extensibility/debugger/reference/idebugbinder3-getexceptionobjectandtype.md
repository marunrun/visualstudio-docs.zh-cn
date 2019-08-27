---
title: IDebugBinder3::GetExceptionObjectAndType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetExceptionObjectAndType
helpviewer_keywords:
- IDebugBinder3::GetExceptionObjectAndType method
ms.assetid: 2a313fe1-4ee1-4f01-af86-382d6c661a8f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 29aa44bdd67234dec4b560ad41be8c677e4356e3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327080"
---
# <a name="idebugbinder3getexceptionobjectandtype"></a>IDebugBinder3::GetExceptionObjectAndType
如果有，则此方法检索与对象关联的异常。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExceptionObjectAndType(
   IDebugObject** ppException,
   IDebugField**  ppField
);
```

```csharp
int GetExceptionObjectAndType(
   out IDebugObject ppException,
   out IDebugField  ppField
);
```

## <a name="parameters"></a>参数
`ppException`\
[out]返回表示异常的对象。

`ppField`\
[out]返回表示可能导致的异常 （可能为 null 值） 的特定字段的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

> [!NOTE]
> 若要验证是否存在异常，请检查返回的值`ppException`： 如果它是一个 null 值，则任何异常不是与此对象相关联。

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)