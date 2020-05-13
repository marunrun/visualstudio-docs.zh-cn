---
title: 操作模式 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 027152b2b2fc18b509a687220e5d963ea1b7e721
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738282"
---
# <a name="operational-modes"></a>操作模式
IDE 可以操作三种模式，如下所示：

- [设计模式](#vsconoperationalmodesanchor1)

- [运行模式](#vsconoperationalmodesanchor2)

- [中断模式](#vsconoperationalmodesanchor3)

  自定义调试引擎 （DE） 如何在这些模式之间转换是一个实现决策，需要您熟悉转换机制。 DE 可以直接实现这些模式，也可能不直接实现这些模式。 这些模式实际上是基于用户操作或 DE 事件切换的调试包模式。 例如，从运行模式到中断模式的过渡是由 DE 的停止事件引起的。 从中断到运行模式或步进模式的过渡由执行操作（如步长或执行）的用户发起。 有关 DE 转换的详细信息，请参阅[执行控制](../../extensibility/debugger/control-of-execution.md)。

## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a>设计模式
 设计模式是 Visual Studio 调试的非运行状态，在此期间您可以在应用程序中设置调试功能。

 在设计模式下只使用几个调试功能。 开发人员可以选择设置断点或创建监视表达式。 当 IDE 处于设计模式时，从不加载或调用 DE。 仅在运行和中断模式下与 DE 交互。

## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a>运行模式
 当程序在 IDE 中的调试会话中运行时，将发生运行模式。 应用程序运行到终止，直到断点被击中，或直到引发异常。 当应用程序运行到终止时，DE 将转换为设计模式。 当断点被击中或引发异常时，DE 将转换到中断模式。

## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a>中断模式
 暂停执行调试程序时，将发生中断模式。 中断模式为开发人员在中断时提供应用程序的快照，并允许开发人员分析应用程序的状态并更改应用程序的运行方式。 开发人员可以查看和编辑代码、检查或修改数据、重新启动应用程序、结束执行或从同一点开始继续执行。

 当 DE 发送同步停止事件时，将进入中断模式。 同步停止事件（也称为停止事件）通知会话调试管理器 （SDM） 和 IDE 正在调试的应用程序已停止执行代码。 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)和[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)接口是停止事件的示例。

 停止事件由调用以下方法之一继续，这些方法之一将调试器从中断模式转换为运行模式或步进模式：

- [执行](../../extensibility/debugger/reference/idebugprocess3-execute.md)

- [步骤](../../extensibility/debugger/reference/idebugprocess3-step.md)

- [继续](../../extensibility/debugger/reference/idebugprocess3-continue.md)

### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a>步进模式
 当程序步进下一行代码或进入、越过或退出函数时，将发生步长模式。 步骤通过调用 方法[步骤](../../extensibility/debugger/reference/idebugprocess3-step.md)执行。 此方法需要`DWORD`指定[STEPUNIT](../../extensibility/debugger/reference/stepunit.md)和[STEPKIND](../../extensibility/debugger/reference/stepkind.md)枚举作为输入参数的 s。

 当程序成功步进下一行代码或函数，或运行到游标或设置的断点时，DE 会自动转换回中断模式。

## <a name="see-also"></a>请参阅
- [执行控制](../../extensibility/debugger/control-of-execution.md)
