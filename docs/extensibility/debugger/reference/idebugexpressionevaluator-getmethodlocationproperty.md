---
title: IDebug表达式评估器：：获取方法定位属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6ba87d6c1a1f7370ce5e209440589f362b87035
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729521"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
此方法将方法位置和偏移转换为内存地址。

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
[在]方法位置和偏移，表示为字符串。

`pSymbolProvider`\
[在]符号提供程序表示为[IDebugSymbol 提供程序](../../../extensibility/debugger/reference/idebugsymbolprovider.md)对象。

`pAddress`\
[在]方法中的地址，表示为[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象。

`pBinder`\
[在]活页夹表示为[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象。

`ppProperty`\
[出]返回表示内存地址的[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 例如，返回的地址可用于设置断点。

 尽管名称`upstrFullyQualifiedMethodPlusOffset`，此参数可以传递一个部分限定的方法名称。 在这种情况下，所选方法是包含 的方法`pAddress`。 如何解释此参数由表达式赋值器及其支持的语言的实现决定。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
