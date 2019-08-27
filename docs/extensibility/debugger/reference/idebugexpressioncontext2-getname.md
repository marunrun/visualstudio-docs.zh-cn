---
title: IDebugExpressionContext2::GetName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2::GetName
helpviewer_keywords:
- IDebugExpressionContext2::GetName
ms.assetid: c2b70d22-17af-4986-a7e3-930910367216
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d53d7f497700d4e23587927adc0c2cee37824daa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325867"
---
# <a name="idebugexpressioncontext2getname"></a>IDebugExpressionContext2::GetName
检索评估上下文的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName( 
   BSTR* pbstrName
);
```

```csharp
int GetName( 
   out string pbstrName
);
```

## <a name="parameters"></a>参数
`pbstrName`\
[out]返回计算上下文的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 名称是此计算上下文的描述。 它通常是指可以通过将引用此确切评估上下文的表达式计算器分析。 例如，在C++的名称是按如下所示：

```
"{ function-name, source-file-name, module-file-name }"
```

## <a name="see-also"></a>请参阅
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)