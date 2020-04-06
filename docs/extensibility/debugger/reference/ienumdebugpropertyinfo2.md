---
title: IEnumDebug属性信息2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715356"
---
# <a name="ienumdebugpropertyinfo2"></a>IEnumDebugPropertyInfo2
此接口枚举[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构。

## <a name="syntax"></a>语法

```
IEnumDebugPropertyInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示特定属性的信息。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[Enum 儿童](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)以获取表示特定属性的子级的此接口。 调用[Enum属性](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)以获取表示特定堆栈帧属性的此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugPropertyInfo2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)|检索枚举序列中指定数量的[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构。|
|[跳](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-skip.md)|在枚举序列中跳过指定数量的[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构。|
|[重置](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)|获取枚举器中[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构的数量。|

## <a name="remarks"></a>备注
 通常，属性是一个信息层次结构，可以包含名称、值、地址和类型，以及适用于关联的属性对象或堆栈帧的任何其他信息。 有关详细信息[，请参阅 IDebugProperty2。](../../../extensibility/debugger/reference/idebugproperty2.md)

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
