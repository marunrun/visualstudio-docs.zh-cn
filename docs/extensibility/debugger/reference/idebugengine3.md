---
title: IDebugEngine3 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730651"
---
# <a name="idebugengine3"></a>IDebugEngine3
表示 (DE) 控制一个或多个模块的调试的单个调试引擎。

## <a name="syntax"></a>语法

```
IDebugEngine3 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>实施者注意事项
 如果自定义 DE (支持符号) 启用 JustMyCode 状态，则会实现此接口。 如果此接口支持符号和 JustMyCode，则该接口必须由 DE 实现。

## <a name="notes-for-callers"></a>调用方说明
 此接口由会话调试管理器 (SDM) 调用，以便为从中加载符号的位置传递用户选项。 它还被调用以在实例化时设置引擎的 GUID (此 GUID 基于) 引擎注册时间的指标。 SDM 还调用此接口以设置 JustMyCode 状态，并将调试器已知的所有异常设置为指定的状态。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)继承的方法之外，接口还 `IDebugEngine3` 公开以下方法。

|方法|说明|
|------------|-----------------|
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|设置用于搜索调试符号的路径或路径。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|为尚未加载其符号的所有模块加载符号。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|告诉你有关 JustMyCode 信息的信息。|
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|设置指标的取消 GUID。|
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|将当前未完成的所有异常设置为指定状态。|

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
