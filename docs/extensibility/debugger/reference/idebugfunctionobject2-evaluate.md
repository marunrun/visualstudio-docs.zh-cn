---
title: IDebugFunctionObject2::Evaluate |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a830dadd9d24f5ecb815db5a89342c5acd281a9c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313411"
---
# <a name="idebugfunctionobject2evaluate"></a>IDebugFunctionObject2::Evaluate
调用函数，并返回结果值作为对象。

## <a name="syntax"></a>语法

```cpp
HRESULT Evaluate (
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwEvalFlags,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate (
   IDebugObject     ppParams,
   uint             dwParams,
   uint             dwEvalFlags,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>参数
`ppParams`\
[in]一个数组[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)表示输入的参数的对象。 这些参数的每个已通过此界面中使用一种创建方法。

`dwParams`\
[in]中的参数数量`ppParams`数组。

`dwEvalFlags`\
[in]中的标志的组合[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)指定计算的执行方式的枚举。

`dwTimeout`\
[in]指定以毫秒为单位，此方法返回前等待的最长时间。 使用**无限**无限期等待。

`ppResult`\
[out]返回**IDebugObject**表示函数作为对象的值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)