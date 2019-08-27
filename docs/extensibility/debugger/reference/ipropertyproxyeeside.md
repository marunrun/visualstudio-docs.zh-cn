---
title: IPropertyProxyEESide | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide
helpviewer_keywords:
- IPropertyProxyEESide interface
ms.assetid: cf227cf8-39d9-4758-8f7e-a697aebb1926
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f6528b146ad3128dd880e594b25ebb5df88bb8f2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353442"
---
# <a name="ipropertyproxyeeside"></a>IPropertyProxyEESide
此接口提供方法以查看关联的对象上的数据。 此接口是支持的类型可视化工具的一部分。

## <a name="syntax"></a>语法

```
IPropertyProxyEESide : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口以支持类型可视化工具。

## <a name="notes-for-callers"></a>调用方的说明
 调用[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)若要获取此接口。 调用[QueryInterface](/cpp/atl/queryinterface)上[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口，以获得[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 以下方法实现此接口：

|方法|描述|
|------------|-----------------|
|[InitSourceDataProvider](../../../extensibility/debugger/reference/ipropertyproxyeeside-initsourcedataprovider.md)|初始化数据源提供程序，以便可以访问该对象的数据。|
|[GetManagedViewerCreationData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getmanagedviewercreationdata.md)|检索有关对象的程序集的信息。|
|[GetInitialData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getinitialdata.md)|获取对象的初始数据。|
|[CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)|创建的现有数据存储的副本。|
|[InPlaceUpdateObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)|创建到现有的数据存储的引用。|
|[ResolveAssemblyRef](../../../extensibility/debugger/reference/ipropertyproxyeeside-resolveassemblyref.md)|检索包含此对象的程序集的上下文中的特定程序集信息。|

## <a name="remarks"></a>备注
 类型可视化工具使用此接口来访问此接口的一部分的对象与关联的值。 通过访问的数据[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)接口，它提供了数据的只读视图。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)