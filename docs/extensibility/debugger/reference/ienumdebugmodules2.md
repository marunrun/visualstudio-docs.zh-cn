---
title: IEnum调试模块2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2
helpviewer_keywords:
- IEnumDebugModules2
ms.assetid: 4fe28074-a960-41ad-b74d-b57f04c0c0ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 612285aa4d5a249c0f922ccae88d98a7df83187b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716443"
---
# <a name="ienumdebugmodules2"></a>IEnumDebugModules2
此接口枚举模块列表。

## <a name="syntax"></a>语法

```
IEnumDebugModules2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示为程序加载的模块列表。

## <a name="notes-for-callers"></a>呼叫者备注
 可视化工作室调用[EnumModule](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugModules2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)|在枚举序列中检索指定数量的模块。|
|[跳](../../../extensibility/debugger/reference/ienumdebugmodules2-skip.md)|在枚举序列中跳过指定数量的模块。|
|[重置](../../../extensibility/debugger/reference/ienumdebugmodules2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugmodules2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugmodules2-getcount.md)|获取模块数。|

## <a name="remarks"></a>备注
 Visual Studio 主要使用此界面更新 **"模块"** 窗口。

 为了在 Visual Studio 中调试，程序是一个逻辑代码指令序列，可以跨越模块边界，因此需要单个[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的模块列表。 列表中的第一个模块通常包含关联程序的初始入口点。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)
