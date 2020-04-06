---
title: IDebugenumfield |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField
helpviewer_keywords:
- IDebugEnumField interface
ms.assetid: 42f685bf-0f39-47f4-98b0-6022efe2bf97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7885f36a113809e81279498a769e257af4f1cde2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730170"
---
# <a name="idebugenumfield"></a>IDebugEnumField
此接口表示枚举类型。

## <a name="syntax"></a>语法

```
IDebugEnumField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序实现此接口以表示枚举。

## <a name="notes-for-callers"></a>呼叫者备注
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回`FIELD_TYPE_ENUM`，请使用[查询接口](/cpp/atl/queryinterface)从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口获取此接口。

## <a name="methods-in-vtable-order"></a>按 VTable 顺序排列的方法
 除了 和`IDebugField``IDebugContainerField`接口上的方法之外，此接口还实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|返回描述此枚举类型名称的[IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)|
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|返回与给定值关联的枚举常量的名称。|
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|返回与给定枚举常量名称关联的值|
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|返回与给定枚举常量名称关联的值，但忽略大小写。|

## <a name="remarks"></a>备注
 它是实际绑定到具有[绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)的位置的基础符号。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)
