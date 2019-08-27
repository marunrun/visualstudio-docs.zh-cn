---
title: IEEVisualizerService::GetPropertyProxy |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetPropertyProxy
helpviewer_keywords:
- IEEVisualizerService::GetPropertyProxy method
ms.assetid: 748750f4-76e7-4580-9da2-afba07681b37
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 117cffcaffc44b37f977aa0d2a195047449edb02
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350125"
---
# <a name="ieevisualizerservicegetpropertyproxy"></a>IEEVisualizerService::GetPropertyProxy
此方法返回属性对象的代理。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPropertyProxy(
   DWORD                  dwID,
   IPropertyProxyEESide** proxy
);
```

```csharp
int GetPropertyProxy(
   uint                     dwID,
   out IPropertyProxyEESide proxy
);
```

## <a name="parameters"></a>参数
`dwID`\
[in]要检索的属性代理的 ID。

`proxy`\
[out]所需的代理中实现[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)接口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
- [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)将请求传递给此方法作为其支持的一部分的类型可视化工具。

## <a name="see-also"></a>请参阅
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)