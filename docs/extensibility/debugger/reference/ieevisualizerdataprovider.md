---
title: IEE可视化数据提供商 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a10f306b6c507f6db7add17931b8a38d926a37d9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718049"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口提供通过类型可视化工具更改对象值的功能。

## <a name="syntax"></a>语法

```
IEEVisualizerDataProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器实现此接口以支持通过类型可视化器修改属性对象上的数据。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口用于通过调用[创建可视化](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)服务创建[IEEVisualizer 服务](../../../extensibility/debugger/reference/ieevisualizerservice.md)对象。 有关详细信息[，请参阅可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法

|方法|描述|
|------------|-----------------|
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|确定是否可以更新此可视化工具表示的对象（以及随后的其值）。|
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|强制重新评估此可视化工具的对象。|
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|获取此可视化工具的现有对象（未执行任何评估）。|
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|更新此可视化工具的对象，从而更改可视化工具提供的值。|

## <a name="remarks"></a>备注
 可视化工具服务（由[IEEVisualizer 服务](../../../extensibility/debugger/reference/ieevisualizerservice.md)接口表示并由[CreateVisualizer 服务](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)返回）保留对实现该接口的对象的`IEEVisualizerDataProvider`引用。 因此，`IEEVisualizerDataProvider`如果该对象维护对`IEEVisualizerService`对象的引用，则接口不应在实现[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)的同一对象上实现：循环引用结果，并在对象被销毁时发生死锁。 建议的方法是在对象委托给的`IEEVisualizerDataProvider`单独对象上实现，`IDebugProperty2`而不调用`IUnknown::AddRef`它。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
