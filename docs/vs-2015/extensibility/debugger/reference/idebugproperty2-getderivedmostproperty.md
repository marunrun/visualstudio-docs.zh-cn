---
title: IDebugProperty2::GetDerivedMostProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetDerivedMostProperty
helpviewer_keywords:
- IDebugProperty2::GetDerivedMostProperty
ms.assetid: cc86b461-62d1-4340-8209-c65037fd8b02
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fde68c090de11d6b479ea0587843a3d4a9d21f94
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68164942"
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

#### <a name="parameters"></a>参数
 `ppDerivedMost`

 [out]返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)表示派生程度最大属性的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`S_GETDERIVEDMOST_NO_DERIVED_MOST`如果不存在派生程度最大属性来检索。

## <a name="remarks"></a>备注
 例如，如果此属性描述一个对象，实现`ClassRoot`这是实际的实例化，但`ClassDerived`派生自`ClassRoot`，则此方法返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象描述`ClassDerived`对象。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)