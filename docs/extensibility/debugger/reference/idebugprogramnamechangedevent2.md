---
title: IDebugProgramNameChangedEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramNameChangedEvent2 interface
ms.assetid: be1f1cd5-0b2f-435c-a052-dca28a7c978d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3b0b1ff52523a91bfa15192de56dfdc6f0f58354
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351189"
---
# <a name="idebugprogramnamechangedevent2"></a>IDebugProgramNameChangedEvent2
从调试引擎 (DE) 会话调试管理器 (SDM) 更改时发送程序的名称。

## <a name="syntax"></a>语法

```
IDebugProgramNameChangedEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口的程序的名称已更改的报告。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问**IDebugEvent2**接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建并发送此事件对象来报告程序名称更改。 DE 发送该事件通过使用[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。 自定义端口供应商发送此事件，使用我的接口。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll