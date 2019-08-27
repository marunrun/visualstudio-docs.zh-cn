---
title: IDebugExpressionEvaluator::GetMethodLocationProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: faa2767e54e9821c7b3270fa60f5be232a2c232f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325768"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
此方法转换为方法位置和偏移量的内存地址。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMethodLocationProperty( 
   LPCOLESTR             upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodLocationProperty(
   string               upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   out IDebugProperty2  ppProperty
);
```

## <a name="parameters"></a>参数
`upstrFullyQualifiedMethodPlusOffset`\
[in]方法的位置和偏移量，表示为字符串。

`pSymbolProvider`\
[in]符号提供程序以表示[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)对象。

`pAddress`\
[in]在方法中，表示为一个地址[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象。

`pBinder`\
[in]此联编程序表示为[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象。

`ppProperty`\
[out]返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)表示的内存地址的接口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 返回的地址可以用于设置断点，例如。

 不管名称如何`upstrFullyQualifiedMethodPlusOffset`，此参数可以传递部分限定的方法名称。 在这种情况下，所选的方法是包含一个`pAddress`。 如何解释此参数是由该表达式计算器和它所支持的语言的实现。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)