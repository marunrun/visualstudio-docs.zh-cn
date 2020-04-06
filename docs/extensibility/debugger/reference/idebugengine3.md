---
title: IDebugEngine3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7026156eac7f60e7435e32244c3cc03ae5f08e1e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730651"
---
# <a name="idebugengine3"></a>IDebugEngine3
表示控制一个或多个模块调试的单个调试引擎 （DE）。

## <a name="syntax"></a>语法

```
IDebugEngine3 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由自定义 DE 实现（如果它支持符号）以启用 JustMyCode 状态。 如果 DE 支持符号和 JustMyCode，则必须实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 会话调试管理器 （SDM） 调用此接口，以传递加载符号的位置的用户选项。 在实例化引擎时，还调用它来设置引擎的 GUID（此 GUID 基于发动机注册时的指标）。 SDM 还会调用此接口以设置 JustMyCode 状态，并将调试器已知的所有异常设置为指定状态。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)继承的方法外，`IDebugEngine3`接口还公开了以下方法。

|方法|描述|
|------------|-----------------|
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|设置 DE 将用于搜索调试符号的路径。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|加载尚未加载其符号的所有模块的符号。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|向 DE 提供有关 JustMyCode 信息的信息。|
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|从指标设置 DE GUID。|
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|将当前未完成的所有异常设置为指定状态。|

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
