---
title: IDebugField |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField
helpviewer_keywords:
- IDebugField interface
ms.assetid: adecdd1c-b1b9-4027-92da-74cbe910636f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8c7a25246f42d288020481330fe60e312849862d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728750"
---
# <a name="idebugfield"></a>IDebugField
此接口表示一个字段，即符号或类型的说明。

## <a name="syntax"></a>语法

```
IDebugField : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序实现此接口作为所有字段的基类。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口是所有字段的基类。 基于[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)的返回值，此接口可以使用查询接口返回更专用[的接口](/cpp/atl/queryinterface)。 此外，许多接口返回来自`IDebugField`各种方法的对象。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugField`。

|方法|描述|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|获取有关符号或类型的可显示信息。|
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|获取字段的种类。|
|[获取类型](../../../extensibility/debugger/reference/idebugfield-gettype.md)|获取字段的类型。|
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|获取字段的容器。|
|[获取地址](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|获取字段的地址。|
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|获取字段的大小（以字节为单位）。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|获取有关字段的扩展信息。|
|[等于](../../../extensibility/debugger/reference/idebugfield-equal.md)|比较两个字段。|
|[获取类型信息](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|获取有关符号或类型的类型无关的信息。|

## <a name="remarks"></a>备注
 类型等效于 C 语言`typedef`。

 在以下C++语言示例中，`weather`是类类型，并且`sunny``stormy`是 符号：

```cpp
class weather;
weather sunny;
weather stormy;
```

 字段是否表示符号或类型可以通过调用[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)并检查[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)结果来确定。 如果设置了`FIELD_KIND_TYPE`位，则字段为类型，如果`FIELD_KIND_SYMBOL`位已设置，则该字段为符号。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
