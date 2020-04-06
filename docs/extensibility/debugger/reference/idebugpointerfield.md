---
title: IDebugPointerfield |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField
helpviewer_keywords:
- IDebugPointerField interface
ms.assetid: d51bd5b2-f18e-4e27-b4fb-e6f652fbf635
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a69797cc513b96c364f0357f22788fc9bcd65657
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725597"
---
# <a name="idebugpointerfield"></a>IDebugPointerField
此接口表示指针类型。

## <a name="syntax"></a>语法

```
IDebugPointerField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序实现此接口以表示指针。

## <a name="notes-for-callers"></a>呼叫者备注
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回`FIELD_TYPE_POINTER`，请使用[查询接口](/cpp/atl/queryinterface)从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口获取此接口。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 除了 和`IDebugField``IDebugContainerField`接口上的方法之外，此接口还实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetDereferencedField](../../../extensibility/debugger/reference/idebugpointerfield-getdereferencedfield.md)|返回描述指针目标的[IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)|

## <a name="remarks"></a>备注
 在 C/C++ 中，如果指针与数组表示法一起使用，则可以是容器。 例如，给定`char *pString`的`pString`具有指向`char`的指针类型。 `pString[3]`具有容器的类型，该容器是引用`char`该容器的第四个元素的指针。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
