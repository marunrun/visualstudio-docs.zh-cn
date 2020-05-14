---
title: IDebug容器字段 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField
helpviewer_keywords:
- IDebugContainerField interface
ms.assetid: a8bbe061-c382-4fe9-a193-3f7d12216041
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a72296517a64c6dcfcb8e347fb00588504aa75a4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733217"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
此接口表示符号或类型，该符号或类型是其他符号或类型的容器。

## <a name="syntax"></a>语法

```
IDebugContainerField : IDebugField
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序在实现[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口的同一对象上实现此接口。 此接口也是表示容器的所有接口的基类。

## <a name="notes-for-callers"></a>呼叫者备注
 许多接口上的许多方法返回此接口。 由于这是所有容器的基类，因此可以使用[QueryInterface](/cpp/atl/queryinterface)从该接口获取更专用的接口。 此类接口包括 IDebugarrayField、IDebugClassfield、IDebugMethodfield 和[IDebugPropertyfield。](../../../extensibility/debugger/reference/idebugpropertyfield.md) [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md) [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|为容器的字段创建枚举器。|

## <a name="remarks"></a>备注
 数组（变量的容器）、类（方法和变量的容器）和方法（参数和局部变量的容器）都是容器的示例。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
