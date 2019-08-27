---
title: 调试引擎 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9e7e5afa4e68d37254c3cb07f1bafa2b48ee787a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336547"
---
# <a name="debug-engine"></a>调试引擎
调试引擎 (DE) 适用于解释程序或操作系统提供调试服务，如执行控制、 断点、 和表达式计算。 DE 负责监视正在调试的程序的状态。 不要为此，DE 使用任何方法可供它在支持的运行时，是否从 CPU 或 Api 提供由运行时。

 例如，公共语言运行时 (CLR) 提供了机制来监视正在运行的程序通过 ICorDebugXXX 接口。 支持 CLR DE 使用适当的 ICorDebugXXX 接口来跟踪正在调试托管的代码程序。 它然后通信会话调试管理器 (SDM) 会转发到此类信息的状态的任何更改[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。

> [!NOTE]
> 调试引擎面向特定的运行时，即，在其中程序正在调试运行的系统。 CLR 是托管代码的运行时，Win32 运行时用于本机 Windows 应用程序。 如果您创建的语言可以为目标的这些两个运行时，一个[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]已提供必要的调试引擎。 您需要实现是表达式计算器。

## <a name="debug-engine-operation"></a>调试引擎操作
 监视服务通过 DE 接口实现，并会导致不同的操作模式之间进行过渡的调试包。 有关详细信息，请参阅[操作模式](../../extensibility/debugger/operational-modes.md)。 通常是只有一个 DE 实现每个运行时环境。

> [!NOTE]
> 尽管有单独的 DE 实现用于为 TRANSACT-SQL 并[!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)]，VBScript 和[!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)]共享单个 DE。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试启用调试引擎以两种方式之一运行： 在与相同的进程[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]shell，或在与目标程序相同的进程正在调试。 当正在调试的进程是实际在解释器下运行的脚本时，通常会出现后一种形式。 调试引擎必须有足够了解的解释器，以便监视脚本。 在这种情况下，该解释器是实际运行时;调试引擎是为特定的运行时实现。 此外，可跨进程和计算机边界 （例如，远程调试） 拆分的单个 DE 实现。

 DE 公开[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试接口。 所有通信都都通过 com。 是否在进程、 进程外或另一台计算机上加载 DE，则它不会影响组件通信。

 DE 适用于以启用该特定运行时的 DE，若要了解表达式的语法的表达式计算器组件。 DE 也可用于访问由语言编译器生成的符号调试信息的符号处理程序组件。 有关详细信息，请参阅[表达式计算器](../../extensibility/debugger/expression-evaluator.md)并[符号提供程序](../../extensibility/debugger/symbol-provider.md)。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算器](../../extensibility/debugger/expression-evaluator.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)