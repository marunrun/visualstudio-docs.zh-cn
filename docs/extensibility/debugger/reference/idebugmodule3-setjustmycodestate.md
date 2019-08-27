---
title: IDebugModule3::SetJustMyCodeState | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::SetJustMyCodeState
helpviewer_keywords:
- IDebugModule3::SetJustMyCodeState
ms.assetid: 68f8166d-ef64-49ae-ad5e-79604f43bbd4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 46a200b91e1680da3f7beac1b0ec4856a39b2564
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323804"
---
# <a name="idebugmodule3setjustmycodestate"></a>IDebugModule3::SetJustMyCodeState
将标记作为或不被用户代码的模块。

## <a name="syntax"></a>语法

```cpp
HRESULT SetJustMyCodeState(
   BOOL fIsUserCode
);
```

```csharp
int SetJustMyCodeState(
   int fIsUserCode
);
```

## <a name="parameters"></a>参数
`fIsUserCode`\
[in]非零值 (`TRUE`) 如果模块应被视为用户代码，零 (`FALSE`) 如果不应。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)