---
title: IDebugProperty2::GetDerivedMostProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetDerivedMostProperty
helpviewer_keywords:
- IDebugProperty2::GetDerivedMostProperty
ms.assetid: cc86b461-62d1-4340-8209-c65037fd8b02
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6b08ca2ad569935a117b8b1255bc740bf395c2ed
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343160"
---
# <a name="idebugproperty2getderivedmostproperty"></a>IDebugProperty2::GetDerivedMostProperty
获取一个属性的派生程度最大属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDerivedMostProperty ( 
   IDebugProperty2** ppDerivedMost
);
```

```csharp
int GetDerivedMostProperty ( 
   out IDebugProperty2 ppDerivedMost
);
```

## <a name="parameters"></a>参数
`ppDerivedMost`\
[out]返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)表示派生程度最大属性的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`S_GETDERIVEDMOST_NO_DERIVED_MOST`如果不存在派生程度最大属性来检索。

## <a name="remarks"></a>备注
 例如，如果此属性描述一个对象，实现`ClassRoot`这是实际的实例化，但`ClassDerived`派生自`ClassRoot`，则此方法返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象描述`ClassDerived`对象。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)