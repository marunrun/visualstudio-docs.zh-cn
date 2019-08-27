---
title: IEEVisualizerDataProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 269f154083f3589e989a6ca2f9ce0835b249181a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350180"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口提供的功能，若要更改类型可视化工具通过对象的值。

## <a name="syntax"></a>语法

```
IEEVisualizerDataProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口以支持在类型可视化工具通过属性对象上修改数据。

## <a name="notes-for-callers"></a>调用方的说明
 此接口可用于创建[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)对象通过调用[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)。 请参阅[可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)的更多详细信息。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法

|方法|描述|
|------------|-----------------|
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|确定是否可以更新此对象 （或以后，其值），表示此可视化工具。|
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|对于此可视化工具将强制重新评估的对象。|
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|获取此可视化工具 （完成的任何评估） 的现有对象。|
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|对于此可视化工具，从而更改可视化工具显示的值更新的对象。|

## <a name="remarks"></a>备注
 可视化工具服务 (由[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)接口，并返回[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)) 中保留对象实现引用`IEEVisualizerDataProvider`接口. 因此，`IEEVisualizerDataProvider`不应在实现的相同对象上实现接口[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)如果该对象将保留对引用`IEEVisualizerService`对象： 循环引用结果和一个当对象被销毁时，会发生死锁。 建议的方法是实现`IEEVisualizerDataProvider`到单独的对象上`IDebugProperty2`对象而无需调用的委托`IUnknown::AddRef`上它。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)