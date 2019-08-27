---
title: IDebugExpressionEvaluator::SetLocale |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::SetLocale
helpviewer_keywords:
- IDebugExpressionEvaluator::SetLocale method
ms.assetid: d3d2027d-74e2-4ae6-bcc7-59d12f873b7c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 18d0dbde0d04dcdf42b3e1fbd19841645036e5bf
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "66325668"
---
# <a name="idebugexpressionevaluatorsetlocale"></a>IDebugExpressionEvaluator::SetLocale
此方法设置要用于创建可打印结果的语言。

## <a name="syntax"></a>语法

```cpp
HRESULT SetLocale( 
   WORD wLangID
);
```

```csharp
int SetLocale(
   ushort wLangID
);
```

## <a name="parameters"></a>参数
`wLangID`\
[in]语言标识符。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法可能会多次调用表达式计算器 (EE) 时加载，因此 EE 必须能够动态切换语言。 EE 使用此区域设置以相应的语言返回错误消息和字符串。

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)