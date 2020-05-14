---
title: IDebug前符号搜索事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9d6f3f78e165ba2f4453131b7b459e3061243ff6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736109"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
调试引擎 （DE） 将此接口发送到会话调试管理器 （SDM）， 以在符号加载期间设置状态栏消息。

## <a name="syntax"></a>语法

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 当 DE 必须在符号加载期间设置状态栏消息时，DE 实现此接口。 此接口仅通过使用脚本解释器或脚本解释器的一部分的调试引擎实现。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现（SDM 使用**查询接口**访问**IDebugEvent2**接口）。

## <a name="notes-for-callers"></a>呼叫者备注
 当 DE 必须在符号加载期间设置状态栏消息时，它创建并发送此事件对象。 该事件使用 SDM 提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调功能在附加到正在调试的程序时发送。

## <a name="methods"></a>方法
 下表显示了 的方法`IDebugBeforeSymbolSearchEvent2`。

|方法|描述|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|检索当前正在调试的模块的名称。|

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
