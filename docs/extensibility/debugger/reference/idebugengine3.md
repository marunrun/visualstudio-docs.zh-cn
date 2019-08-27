---
title: IDebugEngine3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01f15e088635af30bd36919e3da46dee8b8c237b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352446"
---
# <a name="idebugengine3"></a>IDebugEngine3
表示控制一个或多个模块的调试一个单一的调试引擎 (DE)。

## <a name="syntax"></a>语法

```
IDebugEngine3 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口由实现自定义 DE （如果它支持符号） 若要启用的 JustMyCode 状态。 此接口必须由 DE 实现，如果它支持符号和 JustMyCode。

## <a name="notes-for-callers"></a>调用方的说明
 此接口由会话调试管理器 (SDM) 要传递的用户选项要从其加载符号的位置的调用。 它还调用实例化时设置引擎的 GUID （此 GUID 基于指标从引擎注册时）。 SDM 也会调用此接口为 JustMyCode 状态设置并设置指定状态到调试器已知的所有异常。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了继承的方法之外[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)，则`IDebugEngine3`接口公开以下方法。

|方法|描述|
|------------|-----------------|
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|设置 DE 将用于搜索调试符号的路径。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|加载尚无权加载其符号的所有模块的符号。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|有关 JustMyCode 信息告知 DE。|
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|通过度量值设置 DE GUID。|
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|将当前未完成的所有异常都设置为指定的状态。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)