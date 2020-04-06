---
title: IDebug自定义属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute
helpviewer_keywords:
- IDebugCustomAttribute interface
ms.assetid: c5ae41e9-00b9-4cca-871d-b8de9ef390d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a31133139d0104cd29f5d0d0e760bd78ec5783fd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732676"
---
# <a name="idebugcustomattribute"></a>IDebugCustomAttribute
此接口表示自定义属性，它可以提供属性的名称、父级和类类型。

## <a name="syntax"></a>语法

```
IDebugCustomAttribute : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序实现此接口以支持与符号关联的自定义属性。 它通常在其自己的对象上实现。

## <a name="notes-for-callers"></a>呼叫者备注
 对[Next](../../../extensibility/debugger/reference/ienumdebugcustomattributes-next.md)的调用将返回此接口。 对[枚举自定义属性](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)方法的调用返回[IEnumDebug自定义属性接口](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugCustomAttribute`。

|方法|描述|
|------------|-----------------|
|[GetParentField](../../../extensibility/debugger/reference/idebugcustomattribute-getparentfield.md)|获取当前属性附加到的字段。|
|[GetAttributeTypeField](../../../extensibility/debugger/reference/idebugcustomattribute-getattributetypefield.md)|获取自定义属性类类型。|
|[GetName](../../../extensibility/debugger/reference/idebugcustomattribute-getname.md)|获取自定义属性的名称。|
|[GetAttributeBytes](../../../extensibility/debugger/reference/idebugcustomattribute-getattributebytes.md)|将属性信息作为字节 Blob 获取。|

## <a name="remarks"></a>备注
 自定义属性是提供与特定类或方法关联的自定义元数据的 C# 结构。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
