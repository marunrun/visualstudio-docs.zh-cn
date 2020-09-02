---
title: 创建自定义调试引擎 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 241bc016d8a64905951bffef07ba425f1351a727
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903575"
---
# <a name="create-a-custom-debug-engine"></a>创建自定义调试引擎
 (DE) 的调试引擎是允许调试特定运行时体系结构的组件。 每个运行时环境通常只有一个 DE 实现。

> [!NOTE]
> 尽管 Transact-sql 和 JScript 有单独的 DE 实现，但 VBScript 和 JScript 共享了单次 DE。

 DE 与解释器或操作系统一起使用，以提供此类调试服务作为执行控制、断点和表达式计算。 这些服务通过取消接口实现，并可能导致调试器在不同的运行模式之间过渡。 有关详细信息，请参阅 [运行模式](../../extensibility/debugger/operational-modes.md)。

 创建 DE 包含以下步骤：

1. 向 Visual Studio 注册 DE

2. 启用要调试的程序

3. 实现执行控制和状态计算

4. 发送事件

5. 设置终止和分离

## <a name="in-this-section"></a>本节内容
 [注册自定义调试引擎](../../extensibility/debugger/registering-a-custom-debug-engine.md) 说明向 Visual Studio 注册调试引擎以使其可供使用所需的步骤。

 [启用要调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md) 说明在您的 DE 可以调试程序之前，必须先启动 DE，或将其附加到现有的程序。

 [实现执行控制和状态计算](../../extensibility/debugger/execution-control-and-state-evaluation.md) 讨论为什么调试应用程序需要实现执行控制功能。

 [发送事件](../../extensibility/debugger/sending-events.md) 描述调试器和作为基于 DCOM 的事件模型的 DE 之间的通信。

 [设置终止和分离](../../extensibility/debugger/termination-and-detaching.md) 说明如何实现正常终止，这意味着在要调试的应用程序中没有断点、异常、运行时错误或无限循环。

 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md) 记录在调试会话中发生的事件的调用顺序。

 [如何：调试自定义调试引擎](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md) 说明如何调试自定义取消。

## <a name="see-also"></a>另请参阅
- [Visual Studio 调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
