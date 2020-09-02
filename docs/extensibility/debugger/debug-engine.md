---
title: 调试引擎 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a4cb00796f8db23a43cd81a06d80d0fac40f075e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739064"
---
# <a name="debug-engine"></a>调试引擎
调试引擎 (DE) 与解释器或操作系统一起使用来提供调试服务，如执行控制、断点和表达式计算。 DE 负责监视正在调试的程序的状态。 为实现此目的，DE 使用支持的运行时中的任何可用方法，无论是从 CPU 还是由运行时提供的 Api。

 例如，公共语言运行时 (CLR) 提供通过 ICorDebugXXX 接口监视正在运行的程序的机制。 支持 CLR 的 DE 使用适当的 ICorDebugXXX 接口跟踪正在调试的托管代码程序。 然后，它将状态的任何更改传递到会话调试管理器 (SDM) ，后者将此类信息转发到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE。

> [!NOTE]
> 调试引擎以特定的运行时（即在其中运行正在调试的程序的系统）为目标。 CLR 是托管代码的运行时，Win32 运行时用于本机 Windows 应用程序。 如果创建的语言可以作为这两个运行时中的一个运行时，则 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 已提供必要的调试引擎。 只需执行表达式计算器即可实现。

## <a name="debug-engine-operation"></a>调试引擎操作
 监视服务通过取消接口实现，并可能导致调试包在不同的运行模式之间转换。 有关详细信息，请参阅 [运行模式](../../extensibility/debugger/operational-modes.md)。 每个运行时环境通常只有一个 DE 实现。

> [!NOTE]
> 尽管 Transact-sql 和 [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] 、VBScript 和共享单个 de 实现了单独的实现 [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] 。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试使调试引擎可以通过以下两种方式之一运行：在与 shell 相同的进程中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，或在与要调试的目标程序相同的进程中。 如果正在调试的进程实际上是在解释器下运行的脚本，则通常会出现后一种形式。 为了监视脚本，调试引擎必须对解释器有了更深入的了解。 在这种情况下，解释器实际上是一个运行时;调试引擎适用于特定的运行时实现。 此外，可以跨进程和计算机边界拆分单个 DE 的实现 (例如，) 的远程调试。

 DE 公开 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试接口。 所有通信均通过 COM 进行。 无论是在进程内、进程外还是在另一台计算机上加载 DE，都不会影响组件通信。

 DE 与表达式计算器组件一起使用，以使该特定运行时可以了解表达式的语法。 DE 还与符号处理程序组件一起使用，以访问语言编译器生成的符号调试信息。 有关详细信息，请参阅 [表达式计算器](../../extensibility/debugger/expression-evaluator.md) 和 [符号提供程序](../../extensibility/debugger/symbol-provider.md)。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算器](../../extensibility/debugger/expression-evaluator.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)
