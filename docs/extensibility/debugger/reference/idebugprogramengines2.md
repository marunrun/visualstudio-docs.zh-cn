---
title: IDebugProgram引擎2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2
helpviewer_keywords:
- IDebugProgramEngines2 interface
ms.assetid: 53d648f0-6c11-4337-badd-c43f3872b62c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 94df9acc6a0478ba2cb36022bc8618c69be97b8c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722396"
---
# <a name="idebugprogramengines2"></a>IDebugProgramEngines2
程序节点使用此接口来指定可以调试此程序的所有可能的调试引擎 （DE）。

## <a name="syntax"></a>语法

```
IDebugProgramEngines2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 或自定义端口供应商在实现[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)的同一对象上实现此接口，以支持建立用于特定程序的特定 DE。

## <a name="notes-for-callers"></a>呼叫者备注
 在`IDebugProgramNode2`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProgramEngines2`。

|方法|描述|
|------------|-----------------|
|[EnumPossibleEngines](../../../extensibility/debugger/reference/idebugprogramengines2-enumpossibleengines.md)|指示可以调试此程序的所有可能的 D。|
|[SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)|选择要用于调试此程序的 DE。|

## <a name="remarks"></a>备注
 用户选择 DE 后，该选项将调用[SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)注册到程序节点。 选定的引擎成为[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)返回的发动机。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)
