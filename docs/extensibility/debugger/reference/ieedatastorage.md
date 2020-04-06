---
title: IEEData存储 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage
helpviewer_keywords:
- IEEDataStorage interface
ms.assetid: 704e932d-2325-410e-89c4-ce88c6ec19da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad7da71d31e1093d87d68bb39958a71a117f5d5f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718188"
---
# <a name="ieedatastorage"></a>IEEDataStorage
此接口表示字节数组。

## <a name="syntax"></a>语法

```
IEEDataStorage : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器 （EE） 实现此接口以表示字节数组（类型可视化器用于通过[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)接口检索和更改数据）。 EE 通常实现此接口以支持外部类型可视化工具。

## <a name="notes-for-callers"></a>呼叫者备注
 接口上`IPropertyProxyEESide`的方法都返回此接口。 调用[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)以获取[IPropertyProxyEESide 接口](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)。 在[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口上调用[查询接口](/cpp/atl/queryinterface)以获取[IPropertyProxy 提供程序接口](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 接口`IEEDataStorage`实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)|将指定的数据字节数检索到提供的缓冲区。|
|[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)|检索可用数据字节数。|

## <a name="remarks"></a>备注
 此接口由类型可视化器用于访问特定对象持有的数据。 数据被视为字节数组，允许类型可视化器以向用户呈现数据所需的任何方式操作数据。

 如果需要，自定义查看器也可以使用此接口，尽管更通常自定义查看器将使用自定义接口[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)或[GetStringChars（](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)对于面向字符串的数据）。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
