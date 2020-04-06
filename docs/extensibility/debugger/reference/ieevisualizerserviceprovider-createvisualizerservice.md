---
title: IEE可视化服务提供商：：创建可视化服务 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService
helpviewer_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService method
ms.assetid: f366f7c9-358d-46c8-993f-32ff86539833
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e05677122b7d4e4eb025a9382ede1509374de894
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717918"
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
[在][IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象传递给[评估同步](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)。

`pSymProv`\
[在]传递给 的[IDebugSymbol](../../../extensibility/debugger/reference/idebugsymbolprovider.md) `IDebugParsedExpression::EvaluateSync`提供程序对象。

`pAddress`\
[在]传递给[的 IDebug](../../../extensibility/debugger/reference/idebugaddress.md) `IDebugParsedExression::EvaluateSync`地址对象。

`dataProvider`\
[在]实现[IEEVisualizerDataProvider 接口](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)的对象（由表达式赋值器提供）。

`ppService`\
[出]创建的服务。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 和`binder``pSymProv``pAddress`参数都传递给方法`IDebugParsedExpression::EvaluateSync`。 `CreateVisualizerService`仅从`IDebugParsedExpression::EvaluateSync`表达式评估器对类型可视化器的支持调用。

## <a name="see-also"></a>请参阅
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
