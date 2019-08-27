---
title: IDebugBeforeSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 83e71b6059f19840311075261940942010f2e99e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349561"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
调试引擎 (DE) 期间将发送此接口到会话调试管理器 (SDM) 设置的状态消息栏符号加载。

## <a name="syntax"></a>语法

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 它必须在符号加载设置状态条消息时，DE 实现此接口。 只能通过使用或属于脚本解释器的调试引擎实现此接口。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象 (使用 SDM **QueryInterface**访问**IDebugEvent2**接口)。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建并发送此事件对象，它必须在符号加载设置状态条消息时。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时所提供的回调函数。

## <a name="methods"></a>方法
 下表显示的方法`IDebugBeforeSymbolSearchEvent2`。

|方法|描述|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|检索当前正在调试的模块的名称。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll