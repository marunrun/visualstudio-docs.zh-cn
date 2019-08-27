---
title: IEnumDebugPropertyInfo2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2
helpviewer_keywords:
- IEnumDebugPropertyInfo2
ms.assetid: fdea8262-40b8-473e-88ba-639e4c4648e6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cbf6e2f5c644f340ca2c1ebba1d53fc026b0534b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322698"
---
# <a name="ienumdebugpropertyinfo2"></a>IEnumDebugPropertyInfo2
此接口枚举[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构。

## <a name="syntax"></a>语法

```
IEnumDebugPropertyInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口来表示特定属性的信息。

## <a name="notes-for-callers"></a>调用方的说明
 调用[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)获取此接口表示特定属性的子级。 调用[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)获取此接口表示特定堆栈帧的属性。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IEnumDebugPropertyInfo2`。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)|检索指定的数目的[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)枚举序列中的结构。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-skip.md)|跳过指定的数目的[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)枚举序列中的结构。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-reset.md)|将枚举序列重置到开头。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)|获取数[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)枚举器中的结构。|

## <a name="remarks"></a>备注
 一般情况下，属性是层次结构的名称、 值、 地址和类型，可以包含的信息，以及适用于关联的属性对象或堆栈帧的任何其他信息。 请参阅[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)的更多详细信息。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)