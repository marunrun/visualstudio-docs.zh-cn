---
title: IDebugExpressionEvaluator::SetRegistryRoot | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::SetRegistryRoot
helpviewer_keywords:
- IDebugExpressionEvaluator::SetRegistryRoot method
ms.assetid: 790886d8-1975-4d3c-9a75-cd86c1faf4ca
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3e01c340b571854011966e9feeef116fab0b7d41
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62540506"
---
# <a name="idebugexpressionevaluatorsetregistryroot"></a>IDebugExpressionEvaluator::SetRegistryRoot
此方法设置的注册表根目录。 用于通过并行调试。

## <a name="syntax"></a>语法

```cpp
HRESULT SetRegistryRoot ( 
   LPCOLESTR ustrRegistryRoot
);
```

```csharp
int SetRegistryRoot(
   string ustrRegistryRoot
);
```

#### <a name="parameters"></a>参数
 `ustrRegistryRoot`

 [in]新的注册表根。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 表达式计算器首次实例化和点时指定的注册表根通常设置为特定版本的 Visual Studio 的注册表项 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*X.Y*，其中*X.Y*是版本号)。

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)