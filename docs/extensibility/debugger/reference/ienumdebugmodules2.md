---
title: IEnumDebugModules2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716443"
---
# <a name="ienumdebugmodules2"></a>IEnumDebugModules2
此接口枚举模块列表。

## <a name="syntax"></a>语法

```
IEnumDebugModules2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以表示为程序加载的模块的列表。

## <a name="notes-for-callers"></a>调用方说明
 Visual Studio 将调用 [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) 来获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugModules2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)|检索枚举序列中指定数目的模块。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugmodules2-skip.md)|跳过枚举序列中指定数目的模块。|
|[重置](../../../extensibility/debugger/reference/ienumdebugmodules2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugmodules2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugmodules2-getcount.md)|获取模块的数目。|

## <a name="remarks"></a>备注
 Visual Studio 将主要使用此接口来更新 " **模块** " 窗口。

 为了在 Visual Studio 中进行调试，程序是可跨模块边界的代码指令的逻辑序列，因此需要一个适用于单个 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的模块列表。 列表中的第一个模块通常包含关联程序的初始入口点。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)
