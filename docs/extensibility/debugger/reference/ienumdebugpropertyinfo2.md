---
title: IEnumDebugPropertyInfo2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2
helpviewer_keywords:
- IEnumDebugPropertyInfo2
ms.assetid: fdea8262-40b8-473e-88ba-639e4c4648e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bfa0f8feff6a53b84a6337e5bea8bdc622e19a20
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80715356"
---
# <a name="ienumdebugpropertyinfo2"></a>IEnumDebugPropertyInfo2
此接口枚举 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构。

## <a name="syntax"></a>语法

```
IEnumDebugPropertyInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以表示特定属性的信息。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 可获取表示特定属性的子元素的此接口。 调用 [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) 可获取表示特定堆栈帧属性的此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugPropertyInfo2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)|检索枚举序列中指定数目的 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-skip.md)|跳过枚举序列中指定数目的 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构。|
|[重置](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)|获取枚举器中 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构的数目。|

## <a name="remarks"></a>备注
 通常，属性是信息的层次结构，其中可以包含名称、值、地址和类型，以及任何适用于关联的属性对象或堆栈帧的其他信息。 有关更多详细信息，请参阅 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
