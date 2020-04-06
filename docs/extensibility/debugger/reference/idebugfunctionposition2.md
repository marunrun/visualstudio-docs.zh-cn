---
title: IDebug功能位置2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728308"
---
# <a name="idebugfunctionposition2"></a>IDebugFunctionPosition2
此接口表示源文档中函数的抽象位置。

## <a name="syntax"></a>语法

```
IDebugFunctionPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示函数在源文档中的位置。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口作为[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)联合（特别是[BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)结构）的一部分提供，该联合是[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)结构的一部分，用于创建挂起的断点。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugFunctionPosition2`。

|方法|描述|
|------------|-----------------|
|[GetFunctionName](../../../extensibility/debugger/reference/idebugfunctionposition2-getfunctionname.md)|获取此位置相对的函数的名称。|
|[GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)|从函数的开头获取偏移量。|

## <a name="remarks"></a>备注
 此接口表示的位置是基于文本的，具体来说，是[一个TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
