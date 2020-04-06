---
title: IProperty代理提供商 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider
helpviewer_keywords:
- IPropertyProxyProvider interface
ms.assetid: 52e9f7fc-6fe0-4d23-890b-5673dca8c3cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f71d993c7f99cade5b866e67298132a325986e3a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714794"
---
# <a name="ipropertyproxyprovider"></a>IPropertyProxyProvider
此接口提供代理接口来查看和更改对象的数据。

## <a name="syntax"></a>语法

```
IPropertyProxyProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器 （EE） 在实现[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口的同一对象上实现此接口，作为 EE 支持类型可视化器的一部分。

## <a name="notes-for-callers"></a>呼叫者备注
 在`IDebugProperty3`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 接口`IPropertyProxyProvider`实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)|检索属性代理接口以查看对象上的数据。|

## <a name="remarks"></a>备注
 尽管 EE 实现了此接口，但[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)的实现通常由[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)处理。 有关获取 IEE 可视化服务接口的详细信息，请参阅[可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
