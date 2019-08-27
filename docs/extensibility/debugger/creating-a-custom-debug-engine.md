---
title: 创建自定义调试引擎 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3756eb105ec562d902d4631318e7a5fc698601a2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345301"
---
# <a name="create-a-custom-debug-engine"></a>创建自定义调试引擎
调试引擎 (DE) 是允许调试特定运行时体系结构的组件。 通常是只有一个 DE 实现每个运行时环境。

> [!NOTE]
> 虽然有单独的 DE 实现 TRANSACT-SQL 和 JScript，VBScript 和 JScript 共享单个 DE。

 部署适用于解释器或操作系统提供执行控制、 断点、 和表达式计算等调试服务。 这些服务通过 DE 接口实现，并可能会导致调试程序对不同的操作模式之间的转换。 有关详细信息，请参阅[操作模式](../../extensibility/debugger/operational-modes.md)。

 创建部署包含以下步骤：

1. 通过 Visual Studio 注册 DE

2. 启用要进行调试的程序

3. 实现执行控制和状态评估

4. 发送事件

5. 设置终止和分离

## <a name="in-this-section"></a>本节内容
 [注册自定义调试引擎](../../extensibility/debugger/registering-a-custom-debug-engine.md)介绍使用 Visual Studio 注册调试引擎，可以使用它所需的步骤。

 [启用要进行调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)说明你 DE 可调试的程序之前，必须首先启动 DE 或将其附加到现有的程序。

 [实现执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)讨论为什么要调试的应用程序要求实现执行控制功能。

 [将事件发送](../../extensibility/debugger/sending-events.md)描述通信在调试器和 DE 之间作为事件模型基于 DCOM。

 [设置终止和分离](../../extensibility/debugger/termination-and-detaching.md)介绍了如何实现正常终止，这不意味着任何断点、 异常、 运行时错误或要进行调试的应用程序中的无限循环。

 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)记录调试会话中发生的事件的调用顺序。

 [如何：调试自定义调试引擎](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md)说明如何调试自定义部署。

## <a name="see-also"></a>请参阅
- [Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)