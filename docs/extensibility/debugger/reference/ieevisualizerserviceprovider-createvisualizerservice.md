---
title: IEEVisualizerServiceProvider::CreateVisualizerService | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService
helpviewer_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService method
ms.assetid: f366f7c9-358d-46c8-993f-32ff86539833
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 20a8180283e596eeb9dd4ee1391e6e8fe6666829
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310165"
---
# <a name="ieevisualizerserviceprovidercreatevisualizerservice"></a>IEEVisualizerServiceProvider::CreateVisualizerService
此方法创建可视化工具服务。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateVisualizerService(
   IDebugBinder*              binder,
   IDebugSymbolProvider*      pSymProv,
   IDebugAddress*             pAddress,
   IEEVisualizerDataProvider* dataProvider,
   IEEVisualizerService**     ppService
);
```

```csharp
int CreateVisualizerService(
   IDebugBinder binder,
   IDebugSymbolProvider      pSymProv,
   IDebugAddress             pAddress,
   IEEVisualizerDataProvider dataProvider,
   out IEEVisualizerService  ppService
);
```

## <a name="parameters"></a>参数
`binder`\
[in][IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象传递给[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)。

`pSymProv`\
[in][IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)对象传递给`IDebugParsedExpression::EvaluateSync`。

`pAddress`\
[in][IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象传递给`IDebugParsedExression::EvaluateSync`。

`dataProvider`\
[in]一个对象，实现[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)接口 （由表达式计算器提供）。

`ppService`\
[out]已创建的服务。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 `binder`， `pSymProv`，并`pAddress`参数已传递给`IDebugParsedExpression::EvaluateSync`方法。 `CreateVisualizerService` 是仅从调用`IDebugParsedExpression::EvaluateSync`作为类型可视化工具的表达式计算器支持的一部分。

## <a name="see-also"></a>请参阅
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)