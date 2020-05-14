---
title: IEE可视化服务提供商 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider
helpviewer_keywords:
- IEEVisualizerServiceProvider interface
ms.assetid: 859d1a51-1c65-4c8b-ae74-3b74b181ebcd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44d8a73589a4248736ac6c4d73814166056a1f90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717885"
---
# <a name="ieevisualizerserviceprovider"></a>IEEVisualizerServiceProvider
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口允许访问一个可以创建可视化工具服务的方法，该服务用于处理 IDE 的类型可视化器任务。

## <a name="syntax"></a>语法

```
IEEVisualizerServiceProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 Visual Studio 实现此接口以创建可视化工具服务对象，而可视化对象又用于向 Visual Studio IDE`CLSID`提供类型可视化器的类 IDE。

## <a name="notes-for-callers"></a>呼叫者备注
 表达式赋值器 （EE） 调用[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)以获取此接口。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法

|方法|描述|
|------------|-----------------|
|[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)|创建可视化工具服务|

## <a name="remarks"></a>备注
 该`IEEVisualizerServiceProvider`接口是在[实现评估同步](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)期间获得的。 此接口创建的可视化工具服务用于向[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口提供功能，EE 负责实现该接口。 EE 还负责实现[IEE 可视化数据提供程序](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)接口，该接口允许类型可视化器查看和修改属性的值。

 有关这些接口如何交互的详细信息，请参阅[可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
