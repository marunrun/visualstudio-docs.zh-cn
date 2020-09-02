---
title: IDebugFunctionPosition2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionPosition2
helpviewer_keywords:
- IDebugFunctionPosition2 interface
ms.assetid: a835f65b-91b0-48ad-8485-04534c814b1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c260b6316207b0079a2ca8893b851db8b1288ba6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728308"
---
# <a name="idebugfunctionposition2"></a>IDebugFunctionPosition2
此接口表示函数在源文档中的抽象位置。

## <a name="syntax"></a>语法

```
IDebugFunctionPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以表示函数在源文档中的位置。

## <a name="notes-for-callers"></a>调用方说明
 此接口作为 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 联合的一部分提供 (具体来说，这是一个 [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) 结构) ，后者又是 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 结构的一部分，用于创建挂起的断点。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugFunctionPosition2` 。

|方法|说明|
|------------|-----------------|
|[GetFunctionName](../../../extensibility/debugger/reference/idebugfunctionposition2-getfunctionname.md)|获取与此位置相关的函数的名称。|
|[GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)|获取距函数开头的偏移量。|

## <a name="remarks"></a>备注
 此接口表示的位置是基于文本的，尤其是 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 结构。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
