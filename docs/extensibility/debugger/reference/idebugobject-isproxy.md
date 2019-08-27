---
title: IDebugObject::IsProxy |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugObject::IsProxy
- IsProxy
ms.assetid: 06c66b87-db95-4400-ab26-5d33e743a439
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e72df4bd42df8d060ffab5f5ba5a2f44cbc06f9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323424"
---
# <a name="idebugobjectisproxy"></a>IDebugObject::IsProxy
确定对象是否透明代理。

## <a name="syntax"></a>语法

```cpp
HRESULT IsProxy (
   BOOL* pfIsProxy
);
```

```csharp
int IsProxy (
   out bool pfIsProxy
);
```

## <a name="parameters"></a>参数
`pfIsProxy`\
[out]`TRUE`的对象是否透明代理; 否则为`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 默认情况下实现此方法C++调试引擎。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)